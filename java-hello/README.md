# How to create a Java callout

This document provides guidance on when to use a Java callout in Apigee, and situations where other approaches may be more appropriate.

Consider alternative approaches
Before using a Java callout, it's important to consider alternative approaches. For lightweight operations, such as HTTP API calls to remote services, consider using the ServiceCallout policy. For simple interactions with message content, such as modifying or extracting HTTP headers, parameters, or message content, JavaScript or PythonScript policies can be used.

# Java callout capabilities
A Java callout supports the following operations:

Examining or manipulating request or response messages
Getting and setting flow variables
Calling external services
Raising faults
Manipulating error messages and status codes
Java callout limitations
There are certain limitations to what can be done with a Java callout. Most system calls are disallowed, such as making internal file system reads or writes. You also cannot access information about the current process, the process list, or CPU/memory utilization on the machine. Accessing the source code in expressions-1.0.0.jar and message-flow-1.0.0.jar is also not allowed.

It's important to avoid using or relying on Java libraries that are included with Apigee, as they are only intended for Apigee product functionality and may not be available from release to release. If such libraries are used, they should only be used in non-production demonstrations.

# Hello Java callout example

As an example, this document provides a basic "hello world" Java callout. The callout returns a "hello world" response in one of two ways:

If a "username" header with a "name" value is passed in, the callout returns: "Hello, <name>!"
If the header is omitted, the callout returns: "Hello, Guest!"
For implementation details, refer to the example code in the documentation.

# Deploy 

Execute the script java-hello/buildsetup.sh. This script installs the required JAR dependencies in your local Maven repo.

Change to the java-hello/callout directory.

Execute Maven:

````
"mvn clean package"

````

# Deploy and Test the API Proxy
Follow these steps to deploy and test the API proxy:

Change to the "java-hello" directory.

Zip the API proxy bundle:

````
"zip apiproxy-bundle.zip -r apiproxy -x \*.\*~"

````
Upload the proxy bundle to an environment in your Apigee organization. See Creating an API proxy. Be sure to use the "Upload Proxy Bundle" option.

When the proxy is deployed, try calling it with the following command:

````
curl https://$HOSTNAME/java-hello -H "username:Will"

````

This should return "Hello, Will!".