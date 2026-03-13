# Implement the integration flow

## Create the sender connection

In this step, you define your sender channel and sender adapter. In this case, we use an HTTPS sender adapter.

1. Select the **Sender** component. Create the sender channel by dragging the **arrow icon** of the **Sender** ...

<br>![](/exercises/ex2/images/02_IntegrationFlow_04.png)

2. ... to the **Message Start** event where you drop it.

<br>![](/exercises/ex2/images/02_IntegrationFlow_05.png)

3. In the **Adapter Type** prompt, select the **HTTPS** adapter.

<br>![](/exercises/ex2/images/02_IntegrationFlow_06.png)

4. In the **Properties** section of the **HTTPS** connection, navigate to the **Connection** tab. You may need to move up the Properties sheet if it is minimized. The Properties sheet is the place where you define the parameters for every step in the integration flow.
Maintain the **Address** as follows replacing **XX** with the number assigned to you. Furthermore, deselect the **CSRF Protected** checkbox (this will be selected by default).

```yaml
/userXX/products/details
```

<br>![](/exercises/ex2/images/02_IntegrationFlow_07.png)

## Add a JSON to XML converter

The input to the integration flow is sent in JSON format. At a later point, you communicate to a web shop, which is a OData service that understands only XML.
You use a converter for this JSON to XML conversion. After the input is converted into XML, the message is sent as property information to the OData service to fetch the required product details.

1. Select the **Start** event and select the **plus icon** from the quick menu to add a new flow step right after the **Start** event. Optionally, you can also select the flow steps from the palette (the bar on the top containing integration flow steps).

<br>![](/exercises/ex2/images/02_IntegrationFlow_08.png)

2. In the upcoming **Add flow Step** menu, search for the term **JSON** and select the **JSON to XML Converter** entry.

<br>![](/exercises/ex2/images/02_IntegrationFlow_09.png)

## Add and configure a content modifier to parse the product ID

The Content Modifier allows you to modify a incoming message by changing the content of the data containers that are involved in message processing (message header, message body, or message exchange).
The data written to the message header using a Content Modifier also becomes part of the outbound message addressed to a receiver system.
In our case, we need to parse the product ID from the beforehand converted message body, and store the value in an exchange property which at the end is then used in the OData receiver adapter.

1. Select the beforehand created **JSON to XML Converter** and select the **plus icon** from the quick menu to add a new flow step to the sequence of flow steps.

<br>![](/exercises/ex2/images/02_IntegrationFlow_10.png)

2. In the upcoming **Add flow Step** menu, select the **Content Modifier** entry. It should show up in the **Recommended Steps**. If not, you may search for it.

<br>![](/exercises/ex2/images/02_IntegrationFlow_11.png)

3. In the **Properties** section of the **Content Modifier** step, switch to the **Exchange Property** tab. Add a new exchange property by selecting **Add**. Maintain the parameters as follows:

**Action**: Select **Create** from the drop down.

**Name**
```yaml
productIdentifier
```

**Source Type**: Select **XPath** from the drop down.

**Source Value**
```yaml
//productIdentifier
```

**Data Type**
```yaml
java.lang.String
```

<br>![](/exercises/ex2/images/02_IntegrationFlow_12.png)

## Add a request reply step

Certain integration scenarios might require that Cloud Integration communicates with an external service, retrieves data from it, and further processes the data. In such cases, you can use the request reply step as an exit to connect to the external service.

1. Before you continue modeling your integration flow, you may need to enlarge the integration process pool to provide space for the next flow steps. Then, select the beforehand created **Content Modifier** and add a new **Request Reply** flow step to the sequence of flow steps.

<br>![](/exercises/ex2/images/02_IntegrationFlow_13.png)

2. Move the **Receiver** step below the **Request Reply** step by selecting it and dragging it to the desired position on the editor. You do this to ensure that your integration flow is elegantly designed.

<br>![](/exercises/ex2/images/02_IntegrationFlow_14.png)

3. Connect the **Request Reply** to the **Receiver** by dragging the arrow icon on the **Request Reply** to the **Receiver**.

<br>![](/exercises/ex2/images/02_IntegrationFlow_15.png)

4. In the **Adapter Type** prompt, select **OData**.

<br>![](/exercises/ex2/images/02_IntegrationFlow_16.png)

5. In the **Message Protocol** prompt, select **OData V2**.

<br>![](/exercises/ex2/images/02_IntegrationFlow_17.png)

6. In the **Properties** section of the **OData** connection, navigate to the **Connection** tab and add the following **Address**. This is the URL of the online web shop from which the product details will be fetched.

```yaml
https://refapp-espm-ui-cf.cfapps.eu10.hana.ondemand.com/espm-cloud-web/espm.svc
```

<br>![](/exercises/ex2/images/02_IntegrationFlow_18.png)

7. Switch to the **Processing** tab and choose **Select** in the **Resource Path** field.

<br>![](/exercises/ex2/images/02_IntegrationFlow_19.png)

8. Ensure the connection details are the same and choose **Step 2**.

<br>![](/exercises/ex2/images/02_IntegrationFlow_20.png)

9. Choose the **Select Entity** field and select **Products** from the dropdown list.

<br>![](/exercises/ex2/images/02_IntegrationFlow_21.png)

10. Enable the **Select All Fields** checkbox and choose **Step 3**.

<br>![](/exercises/ex2/images/02_IntegrationFlow_22.png)

11. In the **Filter By** section, choose the **Select Field** icon, then select **Product ID** and then **OK**.

<br>![](/exercises/ex2/images/02_IntegrationFlow_23.png)

12. In the dropdown list of the **Filter By** section, select **Equal**. In the value field, enter the exchange property created beforehand as follows. Then select **Finish**.

```yaml
${property.productIdentifier}
```

<br>![](/exercises/ex2/images/02_IntegrationFlow_24.png)

## Add a content modifier to define the content type

1. After the **Request Reply** step, add a **Content Modifier** to set the proper content type. In the **Properties** section of the **Content Modifier** step, switch to the **Message Header** tab. Add a new header by selecting **Add**. Maintain the parameters as follows:

**Action**: Select **Create** from the drop down.

**Name**
```yaml
content-type
```

**Source Type**: Select **Constant** from the drop down.

**Source Value**
```yaml
application/xml
```

<br>![](/exercises/ex2/images/02_IntegrationFlow_25.png)

## Summary

Now that you have modelled the integration flow, you can deploy and test it.

Continue to - [Step 3 - Deploy and run the integration scenario](../ex3/README.md)
