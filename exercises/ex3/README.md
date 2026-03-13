# Deploy and run the integration scenario

In the following, you will deploy and test the beforehand created integration flow.

## Save and deploy

1. **Save** and **Deploy** your integration flow.

<br>![](/exercises/ex3/images/03_DeployAndRun_01.png)

2. In the upcoming dialog, keep the **Runtime Profile** and confirm the deployment by selecting **Yes**.

<br>![](/exercises/ex3/images/03_DeployAndRun_02.png)

3. Once the integration flow has been deployed, a toast message is displayed at the bottom of the screen. Furthermore, you get the deployment status displayed right below the name of the integration flow.

<br>![](/exercises/ex3/images/03_DeployAndRun_03.png)

4. You can also check the deployment status in the monitor. Navigate to **Monitor > Integrations and APIs** from the menu, and select the tile **Manage Integration Content**.

<br>![](/exercises/ex3/images/03_DeployAndRun_04.png)

5 .In the **Manage Integration Content** page, filter for your ID **XX**. You should see your deployed integration flow in status **Started**. You may select the **Copy entry point URL to clipboard** button next to the integration flow's end point.

<br>![](/exercises/ex3/images/03_DeployAndRun_05.png)

Now you are all set to test your scenario!

## Test and monitor

1. Open the Bruno application on your laptop, expand the **Getting Started** collection and select the POST request **Read Product Details**.
Either change **XX** in the preset URL to the number assigned to you or override the complete URL by pasting the URL from the clipboard in case you did so in the step before.
Then trigger a message by selecting the **Send Request** button on the upper right.

<br>![](/exercises/ex3/images/03_DeployAndRun_06.png)

2. The request should return HTTP code **200** and a response with the product details should be displayed in the **Response** section.

<br>![](/exercises/ex3/images/03_DeployAndRun_07.png)


3. Navigate back to the monitoring page of Cloud Integration. Select your deployed integration flow, and select the link **Monitor Message Processing** to navigate to the **message monitor**.

<br>![](/exercises/ex3/images/03_DeployAndRun_08.png)

4. In the **Monitor Message Processing**, you should see a new log in status **Completed**.

<br>![](/exercises/ex3/images/03_DeployAndRun_09.png)

## Summary

Congratulations. You have successfully created and tested your first integration scenario on Cloud Integration.
