TUTORIAL #4: ADD YOUR APP TO SALESFORCE USING FORCE.COM CANVAS

 

You’ve done a lot already. Let’s go one step further and make your app accessible for your users right from within Salesforce. Force.com Canvas enables you to easily integrate a third-party application in Salesforce. Force.com Canvas is a set of tools and JavaScript APIs that you can use to expose an application as a canvas app. This means you can take your new or existing applications and make them available to your users as part of their Salesforce experience.

Step 1: Update your Application with a New Branch

Earlier, we added a branch to the codebase named “full.” Now we’ll add one named “canvas.”

1. Return to the command line, and make sure you’re in the **spring-mvc-fulfillment-base **folder. 
2. Enter the following command to fetch the canvas branch and merge it with your master branch, all in one step: **   git pull origin canvas**
4. Execute the following command to push the local changes to Heroku: **git push heroku master **
5. In a browser tab or window, navigate to **https://****_{appname}_****.herokuapp.com **to see the changes (refresh your browser if needed). 

**Tell Me More...**

You can review all of the changes brought in by this branch on GitHub at https://github.com/sbob-sfdc/spring-mvc-fulfillment-base/compare/full...canvas.

Notice that the new branch uses the signed request from the Force.com Canvas API and not the Heroku-initiated OAuth from Tutorial 3, Step 2. The new branch also uses the Force.com REST API to manipulate invoice records. Look at CanvasUiController.java in particular to see how it retrieves, parses, and sets the signed request for use by the app. Also, order.jsp has changed to present an easier-to-use screen on the invoice page layout. This tutorial has only set the signed request for use on the canvasui page and the orders page in the app.

Step 2: Edit the Connected App Details and Enable the App for Force.com Canvas

We’ve already configured your connected app. Now we need to enable and configure it for Force.com Canvas.

1. From Setup, click **Create **&gt; **Apps**. 
2. In the Connected App Settings section, select your application and click **Edit**. 
3. In the Canvas App Settings section, select the **Force.com Canvas **checkbox. 
4. In the **Canvas App URL **field, enter **https://****_{appname}_****.herokuapp.com/canvasui**. 
5. In the **Access Method **field, select Signed Request (Post). 
6. In the **Locations **field, select Chatter Tab and Visualforce Page, and then add them to the selected locations. 

 

**7. **Click **Save**.

If you look at CanvasUiController.java, you’ll see something like the following, which shows Heroku obtaining a signed request and validating it. We’re leveraging the OAUTH_CLIENT_SECRET Heroku key set in Tutorial 3, Step 2 to validate the signed request.

@Controller

@RequestMapping(value="/canvasui")

public class CanvasUIController {

    private static final String SIGNED_REQUEST = "signedRequestJson";

    private CanvasContext cc = new CanvasContext();

    @Autowired

    private OrderService orderService;

    @Autowired

    private InvoiceService invoiceService;

    private Validator validator;

    @Autowired

    public CanvasUIController(Validator validator) {

        this.validator = validator;

    }

    @RequestMapping(method= RequestMethod.POST)

public String postSignedRequest(Model model, @RequestParam(value="signed_request")String signedRequest, HttpServletRequest request){

        String srJson = SignedRequest.verifyAndDecodeAsJson

(signedRequest, getConsumerSecret());  

CanvasRequest cr = SignedRequest.verifyAndDecode(signedRequest, getConsumerSecret());

        HttpSession session = request.getSession(true);

        model.addAttribute(SIGNED_REQUEST, srJson);

        cc = cr.getContext();

        CanvasEnvironmentContext ce = cc.getEnvironmentContext();

        Map&lt;String, Object&gt; params = ce.getParameters();

        if (params.containsKey("orderId")) {

            invoiceService.setSignedRequest(cr);

            Integer orderId = Integer.parseInt(params.get("orderId").toString());

            if(orderId != null) {

                Order order = orderService.findOrder(orderId);

                if (order == null) {

                    throw new ResourceNotFoundException(orderId);

                }

                model.addAttribute("order", order);

                Invoice invoice;

                try {

                    invoice = invoiceService.findInvoice(order.getId());

                } catch (ApiException ae) {

                    // No match

                    invoice = new Invoice();

                }

                model.addAttribute("invoice", invoice);

                return "order";

            }

}

        return getOrdersPage(model);

    }

    @RequestMapping(method=RequestMethod.GET)

    public String getOrdersPage(Model model) {

        model.addAttribute("order", new Order());

        model.addAttribute("orders", orderService.listOrders());

        return "orders";

    }

    private static final String getConsumerSecret(){

        String secret = System.getenv("OAUTH_CLIENT_SECRET");

        if (null == secret){

            throw new IllegalStateException("Client secret not found in environment.

            You must define the OAUTH_CLIENT_SECRET environment variable.");

        }

        return secret;

    }

}

After the validation, the signed request is passed to order.jsp, where the browser can access it.

&lt;%@ page session="false" %&gt;

&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %&gt;

&lt;%@ taglib uri="http://java.sun.com/jsp/jstl/fmt" prefix="fmt" %&gt;

&lt;%@ taglib prefix="form" uri="http://www.springframework.org/tags/form" %&gt;

&lt;html&gt;

 &lt;head&gt;

  &lt;title&gt;Order&lt;/title&gt;

  &lt;link rel="stylesheet" href="&lt;c:url value="/resources/blueprint/screen.css" /&gt;"

  type="text/css" media="screen, projection"&gt;

  &lt;link rel="stylesheet" href="&lt;c:url value="/resources/blueprint/print.css" /&gt;"

type="text/css" media="print"&gt;

  &lt;!--[if lt IE 8]&gt;

   &lt;link rel="stylesheet" href="&lt;c:url value="/resources/blueprint/ie.css" /&gt;"

  type="text/css" media="screen, projection"&gt;

  &lt;![endif]--&gt;

  &lt;script type="text/javascript" src="&lt;c:url value="/resources/jquery-1.4.min.js" /&gt; "&gt;

  &lt;/script&gt;

  &lt;script type="text/javascript" src="&lt;c:url value="/resources/json.min.js" /&gt; "&gt;

  &lt;/script&gt;

        &lt;script type="text/javascript" src="&lt;c:url value="/resources/canvas-all.js" /&gt; "&gt;

    &lt;/script&gt;

        &lt;script&gt;

// Get the Signed Request from the CanvasUIController  

var sr = JSON.parse('${not empty signedRequestJson?signedRequestJson:"{}"}');

           // Set handlers for the various buttons on the page

           Sfdc.canvas(function() {

               $('#finalizeButton').click(finalizeHandler);

               $('#deleteButton').click(deleteHandler);

           });

           // This function will be called when the "Finalize" button is clicked.

           // This shows using the Canvas Cross Domain API to hit the REST API

           // for the invoice that the user is viewing.  The call updates the

           // Status__c field to "Shipped".  If successful, the page is refreshed,

           // and if there is an error it will alert the user.

           function finalizeHandler(){

               var invoiceUri=sr.context.links.sobjectUrl + "Invoice__c/${order.id}";

               var body = {"Status__c":"Shipped"};

               Sfdc.canvas.client.ajax(invoiceUri,{

                   client : sr.client,

                   method: 'PATCH',

                   contentType: "application/json",

                   data: JSON.stringify(body),

                   success : function() {

                       window.top.location.href = getRoot() + "/${order.id}";

                   },

                   error: function(){

                       alert("Error occurred updating local status.");

} });

}

           // This function will be called when the "Delete Order" button is clicked.

           // It will delete the record from the Heroku database.

           function deleteHandler(){

               $.deleteJSON("/order/${order.orderId}", function(data) {

                   alert("Deleted order ${order.orderId}");

                   location.href = "/orderui";

               }, function(data) {

                   alert("Error deleting order ${order.orderId}");

});

               return false;

           }

           // This function gets the instance the user is on for a page referesh

           function getRoot() {

               return sr.client.instanceUrl;

           }

&lt;/script&gt;

&lt;/head&gt;

&lt;body&gt;

       &lt;div id="bodyDiv" style="width:inherit;"&gt;

           &lt;div id="myPageBlockTable"&gt;

               &lt;h2 id="OrderTitle"&gt;

                   Order Number: &lt;c:out value="${order.orderId}"/&gt;

not shipped --&gt;

  &lt;col width="20%"&gt;

  &lt;tr&gt;&lt;td class="myCol"&gt;Invoice Id:&lt;/td&gt;&lt;td class="valueCol"&gt;

  &lt;c:out value="${invoice.id}"/&gt;&lt;/td&gt;&lt;/tr&gt;

  &lt;tr&gt;&lt;td class="myCol"&gt;Invoice Number:&lt;/td&gt;&lt;td class="valueCol"&gt;

  &lt;c:out value="${invoice.number}"/&gt;&lt;/td&gt;&lt;/tr&gt;

&lt;tr&gt;&lt;td class="myCol"&gt;Status:&lt;/td&gt;&lt;td class="valueCol" valign="center"&gt;

  &lt;c:out value="${invoice.status}"/&gt;

      &lt;!-- Display a green check if the order is Shipped, or a red x if

      &lt;c:choose&gt;

          &lt;c:when test="${invoice.status == 'Shipped'}"&gt;

              &lt;img src="/resources/images/shipped.png" /&gt;

          &lt;/c:when&gt;

          &lt;c:otherwise&gt;

              &lt;img src="/resources/images/pending.png" /&gt;

          &lt;/c:otherwise&gt;

      &lt;/c:choose&gt;

&lt;/h2&gt;

&lt;table id="myTable" width="100%"&gt;

                    &lt;/td&gt;&lt;/tr&gt;

                &lt;/table&gt;

                &lt;!-- Display the Back and Delete Order Button if viewed outside

                of salesforce (no signed request). --&gt;

                &lt;!-- Display the Finalize Button if viewed inside of salesforce and

                the Status is not Shipped. --&gt;

                &lt;c:choose&gt;

                    &lt;c:when test="${empty signedRequestJson}"&gt;

                        &lt;button onclick="location.href='/orderui'"&gt;Back&lt;/button&gt;

                        &lt;button id="deleteButton"&gt;Delete Order&lt;/button&gt;

                    &lt;/c:when&gt;

                    &lt;c:otherwise&gt;

                        &lt;c:if test="${invoice.status ne 'Shipped'}"&gt;

                            &lt;button id="finalizeButton"&gt;Finalize&lt;/button&gt;

                        &lt;/c:if&gt;

                    &lt;/c:otherwise&gt;

                &lt;/c:choose&gt;

            &lt;/div&gt;

        &lt;/div&gt;

 &lt;/body&gt;

&lt;/html&gt;

Step 3: Configure Access to Your Force.com Canvas App

Because this app is designed for use by a specific audience, let’s give access only to the users who need it.

1. In Salesforce, from Setup, click **Manage Apps **&gt; **Connected Apps**. 
2. Click your app, and then click **Edit**. 
3. In the **Permitted Users **field, select **Admin approved users are pre-authorized**. Click **OK **on the popup message that appears. 
4. Click **Save**. 

Now you’ll use profiles and permission sets to define who can see your canvas app. In this example, we’ll allow anyone with the System Administrator profile to access the app.

**5. 
6. **Your app is now available to anyone with the System Administrator profile.

In the Connected App Detail page’s Profiles related list, click **Manage Profiles**. Select the System Administrator profile, and then click **Save**.

Step 4: Make Your Force.com Canvas App Available from the Chatter Tab

The values you selected in the Locations field when creating the connected app in Step 2: Edit the Connected App Details and Enable the App for Force.com Canvas on page 16 determine where an installed canvas app appears. When an app is made available to the Chatter tab, there’s nothing we need to do for this step. If you log into your Salesforce org and select the Chatter tab, you’ll see that your canvas app appears in the app navigation list.

Note: When displaying the list of orders on the Chatter Tab, remember that orders.jsp has been set up to handle the signed request POST. However, if you click into a record from this page, you are redirected to orderui , which uses OAuth. If the Heroku OAuth flow is inactive, you may receive an error when viewing the individual order.

Click your app’s name. It should look something like this:

Step 5: Use Visualforce to Display the Canvas App on a Record

While you can certainly use the app based on the work completed so far, let’s take one more step and use Visualforce to display information from your canvas app on the invoice record.

1. From Setup, click **Develop **&gt; **Pages**. 
2. Click **New**. 

   

**3. **In Label, enter _FulfillmentCanvas_. You use this label to identify the page in Setup tools when performing actions such as defining custom tabs or overriding standard buttons.

1. In **Name**, accept the default name **_FulfillmentCanvas_**. 
2. Add the following markup to the Visualforce Markup box, making sure to replace **_{appname} _**with your Heroku application name, and then click **Save**. Notice how the parameters tag in the **apex:canvasApp **component is set to **"{'orderId':'{!Invoice__c.OrderId__c}'}"**. This code sends a JSON object as part of the signed request to the Heroku app when the page is loaded. In the signed request, the parameters object will look something like **parameters : {'orderId':'5'}**, where '5' is the OrderId from the invoice record. Remember that this value is an external ID field that connects the record in the Heroku database to the Salesforce invoice record. By delivering the OrderId to the Heroku app with the signed request, the Heroku app can display the correct record on the invoice page layout. Your page should look something like this: Now let’s add your Visualforce page to the page layout. 
3. From the Invoices tab, select a record. 
4. Click **Edit Layout **and then **Visualforce Pages**. 
5. Drag a section down to your page and name it Canvas Fulfillment. 
    1. Make sure to deselect **Edit Page**. 
    2. Select **1–Column **for the layout. 

6. Drag your **FulfillmentCanvas **page onto the new section. 
7. Click the wrench to update your page properties. The width should be set to 100% and height set to 165 pixels. 
8. Ensure that both **Show scrollbars **and **Show label **are deselected and click **Save**. 
9. From Setup, click **Create **&gt; **Objects**, and then click **Invoice**. 

    &lt;apex:page standardController="Invoice__c"&gt;

        &lt;apex:canvasApp developerName="{appname}"

parameters="{'orderId':'{!Invoice__c.OrderId__c}'}" width="100%"/&gt;

    &lt;/apex:page&gt;

**13. **In the Custom Fields & Relationships section, click Status.  
**14. **Add another picklist item named Shipped.  

Now when users go to an invoice record, they’ll see the canvas app right on the record detail page:

Notice the **Finalize **button in the canvas app. If the invoice isn’t in 'Shipped' status, the red “X” and **Finalize **will show in the app. If you click **Finalize**, Heroku uses the Force.com Canvas API to call the REST API and update the invoice Status field. Once the status is set to 'Shipped', the red “X” is replaced and **Finalize **is hidden.

Summary

Congratulations! With a combination of OAuth authentication, Force.com REST API, Apex triggers, @future callouts, the polyglot framework of the Heroku platform, Force.com Canvas, and Visualforce, you created and deployed a bi-directional integration between two clouds.

This workbook covers just one example of the many ways to integrate your applications with Salesforce. One integration technology that we didn’t mention is the Streaming API that lets your application receive notifications from Force.com whenever a user changes Salesforce data. You can use this in the fulfillment application to monitor when changes are made to invoices and to automatically update the application pages accordingly. Visit https://developer.salesforce.com to learn more about all the ways you can integrate your application with Salesforce.

 
