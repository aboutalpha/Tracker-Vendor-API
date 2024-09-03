# Location-Tracking-System-Vendor-Api

<img width="1092" alt="image" src="https://github.com/user-attachments/assets/37853c9b-1472-4cd8-a689-8be68567aa1f">

Twitter-api repo: https://github.com/aboutalpha/Tracker-Twitter
AWS network-config repo: https://github.com/aboutalpha/Tracker-Network

## Overview
This Location Tracker System is designed to track and manage connections and messages between different vendors using DynamoDB, SQS, and WebSockets.

## Project Structure
aws.ts: Contains utility functions for interacting with AWS services, specifically DynamoDB and SQS.
connect.ts: Handles establishing connections between clients and the WebSocket API.
disconnect.ts: Manages disconnections from the WebSocket API and cleans up resources accordingly.
get-vendors.ts: Retrieves vendor information from the DynamoDB table.
send-vendor.ts: Sends vendor-related data to clients via WebSocket messages.

## Setup
Install Dependencies
`npm install`
Environment Variables Create a .env file in the root directory and include the following environment variables:

AWS_REGION=your-aws-region
AWS_TABLE_NAME=your-dynamodb-table-name
AWS_SQS_URL=your-sqs-url
AWS_WEBSOCKET_URL=your-websocket-url

Build Compile the TypeScript files into JavaScript using the following command:

`npm run build`
Deploy
Deploy the compiled files to your AWS environment. Make sure that your AWS credentials are configured correctly.

## File Descriptions
### aws.ts
This module provides utility functions for interacting with DynamoDB and SQS:

dynamodbDescribeTable: Describes the specified DynamoDB table.
dynamodbScanTable: Scans the DynamoDB table, yielding items in batches.
getAllScanResults: Retrieves all results from a DynamoDB scan.
sqsDeleteMessage: Deletes a message from the SQS queue.
broadcastMessageWebsocket: Broadcasts a message to all WebSocket connections.

### connect.ts
This module manages client connections to the WebSocket API:

handler: This function is triggered when a client connects. It records the connection in the DynamoDB table.

### disconnect.ts
This module handles client disconnections from the WebSocket API:

handler: This function is triggered when a client disconnects. It removes the connection from the DynamoDB table.

### get-vendors.ts
This module retrieves vendor information from the DynamoDB table:

handler: This function retrieves all vendors' connection details and sends the data to the WebSocket.

### send-vendor.ts
This module sends vendor data via WebSocket messages:

handler: This function handles incoming SQS messages, retrieves the necessary connection information, and sends the message to all connected clients.

## Usage
Connecting: When a new client connects, the connect.ts handler is triggered, registering the connection in the DynamoDB table.

Disconnecting: When a client disconnects, the disconnect.ts handler removes their connection from the DynamoDB table.

Messaging: Vendor data can be sent through the WebSocket by triggering the send-vendor.ts handler, which broadcasts the message to all connected clients.

## Troubleshooting
Logs: Check CloudWatch logs for any errors or issues with the Lambda functions.
Permissions: Ensure that the necessary IAM roles and permissions are correctly set for accessing DynamoDB, SQS, and API Gateway.
