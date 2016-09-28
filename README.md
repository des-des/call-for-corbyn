# call-for-corbyn

copy of this document: https://hackpad.com/Call-for-Corbyn-miCC5ktloV9

Call for Corbyn

problems to solve
callers want to be anonymous
callers should not need to use their own credit/minutes
callers spend too much time waiting for pickup / going to answer

Here's a first take:
 
Funding proposal: Call for Corybn prototype
 
Caller: momentum/labour member volunteering to make calls
Callee: member of the public being called.
Web client: The web site the caller will be using to register availability.
Asterisk server: responsible for routing calls between the caller and callee
Node server: This will be the glue. managing the asterisk server and the callers session on the web client.
voip: Voice over IP.
 
User flow (caller).
 1. The user downloads a voip app on their phone
 2. The user registers as active on the the web client (they are on the line from this point). For the prototype, the web client will be both minimal and not integrated with the existing call for corybn site. It will not allow the user to enter data after the call  (ben: could be a stretch goal?).
 
 > (Olugbenga) For one touch dialling, it will serve as both a simulator and minimal. This can easily be integrated because it is just one button on the interface. For the predictive dialler, it will be too complicated to integrate and will be a long term effort.
 3. The caller gets connected to a callee.
 4. Once the user has finished making calls they will end their session via the web client. 
and callee numbers, It will act as a controller for the asterisk server, passing the asterisk server Callee numbers, managing the callers sessions and passing active callers


> (Olugbenga) We need to have clarity on how the system will be used. For now I'm assuming the web client will be used by onsite users and road warriors and the app is responsive to cater for smart phone screen sizes. What you have described above is called predictive dialling. The way in which predictive dialling is used in the UK is regulated. Abandoned call rates must not exceed 3% of live calls for any 24-hour period for each campaign. Records must be kept to demonstrate compliance with these requirements. What does this mean for us? It will be difficult to involve road warriors because they are out of a controlled environment where swift call pick ups can be enforced. The feasible approach is to build a systems that serves the road warrior with one touch dialling and predictive dialling for call centre use. 


> (@des-des) I think for now our only target is road warriors. I think we should focus on this use case for now. By road warriors you mean volunteers calling from home? Can you expand on how you think things should work in their case .

What is happening during the user flow.
 1. The user registers as active on the the web client
   1. The user makes a page request to the node server.
   2. The node server responds with the web client.
   3. The user uses the web client to register an active session on the node server.
     > (Olugbenga) Points 2.1 -  2.3 will happen for a one touch dialling but won't do 2.4. It will make a call. For predictive dialling, the callers have no business initiating the calls, the system does that.
   4. The node server tells asterisk to start making calls to the callees.
   5. The Asterisk server makes a connection to the provider.
   6. The Asterisk server begins making calls to callees, via the provider
 
  > (Olugbenga) This doesn't happen through one connection, a connection is made per every call. 
 2.  The caller gets connected to a callee.
   1. When a callee answers a call asterisk will tell the node server it has made a connection.
   2. The node server will respond with the with the information the asterisk server needs to call the user/caller via voip.
The asterisk service is in charge at this point, it does it without any further instructions from the node server.
   3. when the user/caller answers (they should do this quickly) Asterisk will connect the caller and the callee.
Yes for predictive dialling with the potentials for abandoned calls. For one touch dialling the caller will be called first and the caller will be waiting on the callee.
 
Stack:
Docker: The backend will held in a collection of docker containers. This will allow us to easily deploy into the existing infrastructure, while allowing us to scale later.
Asterisk: allows us to route calls and manage all the telephony and pxb
Node (Hapi): Glue for sending numbers to asterisk, webui. Node scales very well, as well as allowing fast prototyping.
Client: For now, we can build a client in plain html/css/js.
 
nb. Node, Docker and Asterisk are all open source projects.
 
Beyond the prototype.
After testing the prototype, depending on what feedback we get, I expect the next steps to go something like:
1. Build out the webui so that the caller can see and enter callee information
2/3. Build call button into webui so the caller can use their browser and not their phone to receive calls.
2/3. Allow the caller to connect to the asterisk server before it connects will the callee, so the callee has zero wait time upon picking up the phone.
 
Then before integration and adoption. building in load balancers, scaling and testing the system under stress.
 
We think we build the prototype in 4 days
End of proposal.

