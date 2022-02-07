# Remote Procedure Call
The request is made by the use of a _client stub._ The stub _assembles (**marshall**)_ the parameters and **send** to the server stub. It **blocks** until receives a response (in a sync scenario).

Then the server stub receives the response, parses the message (_**unmarshall**),_ call the function and after the actual function returns the result, the server stub receives it, _**marshalls**_ it and send back to the client stub.

Upon the reception of the result, the client stub _**unmarshalls**_ the response and give it back to the client.