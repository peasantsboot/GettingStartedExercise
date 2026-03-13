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

## Add and configure a content modifier

The Content Modifier allows you to modify a incoming message by changing the content of the data containers that are involved in message processing (message header, message body, or message exchange).
The data written to the message header using a Content Modifier also becomes part of the outbound message addressed to a receiver system.
In our case, we need to parse the product ID from the beforehand converted message body, and store the value in an exchange property which at the end is then used in the OData receiver adapter.

1. Select the beforehand created **JSON to XML Converter** and select the **plus icon** from the quick menu to add a new flow step to the sequence of flow steps.

<br>![](/exercises/ex2/images/02_IntegrationFlow_10.png)

2. In the upcoming **Add flow Step** menu, select the **Content Modifier** entry. It should show up in the **Recommended Steps**. If not, you may search for it.

<br>![](/exercises/ex2/images/02_IntegrationFlow_11.png)

3. In the **Properties** section of the **Content Modifier** step, switch to the **Exchange Property** tab. Add a new exchange property by selecting **Add**. Maintain the parameters as follows:

## Summary

Now that you have modelled the integration flow, you can deploy and test it.

Continue to - [Step 3 - Deploy and run](../ex3/README.md)
