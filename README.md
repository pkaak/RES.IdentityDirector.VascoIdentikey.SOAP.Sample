# RES.IdentityDirector.VascoIdentikey.SOAP.Sample

Sample use of RES Automation integration with Vasco Identikey Server by using SOAP.

This building block for RES ONE Identity Director has a dependency with the RES.Automation.VascoIdentikey.SOAP.Connector buildingblocks that can be found on the RES Hub. 

This buildingblock installs the following in the RES ONE Identity Director:
Global Table: VascoDomains
Organization: Vasco User and Vasco Token

Services:
- Access Vasco Identikey: This service creates a user on the Vasco Identikey Server. This enables the user to log onto the Vasco portal. This services set the organizational unit of the user to Vasco User and adds the Vasco Domain to the people attribute of the user. When requested the service askes the requester to verify the information and to select the right Vasco Domain and Organizational Unit. 

- Request Digipass: This service first checks available licenses (maximum users that can request the service is set to 2). If there are still licenses, it will claim the first available digipass licenses that can be used and requests the QR code (in base64) and activation code. This information is than stored in the person attributes. After successfull retrieval of the information the Organization Unit of the user is set to Vasco Token. The service than requests another service, called Returntimer Vasco Digipass Subscription. When this service or Access Vasco Identikey service is returned, it will update the Return Vasco Digipass Subscription so that service will terminated within 1 hour.

- Returntimer Vasco Digipass Subscription: This service will run for 48 hours. Every hour an evaluation of the timer takes place to see if 48 hours has been over. If this is the case, the service will return the Request Digipass service. This service can be canceled by updating the timer to 48 hours when the Request Digipass is canceled.

- Get Digipass QR/Activation Code: This service will retreive the QR code and Activation Code for the digipass serial number that is assigned to the user.

- Vasco Domains: This service fills the global table with the Vasco Domains available on the Vasco Identikey Server. Please run this service first after installation of the building blocks, as the global table needs to be filled for other services to function.
	
