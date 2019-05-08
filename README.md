----------------------------------------------------validate swagger document-----------------------------------------------------------------------------------------
swagger-tools validate {swagger file location}
example:
swagger-tools validate C:\Users\Chandra_Gaddam\Desktop\PackageTypeByQuantity.json

-------------------------------------------------generate proxy from openApi specs----------------------------------------------------------------------------------
openapi2apigee generateApi {proxy name} -s {swagger file location} -d {cerated proxy destination}
I have stored the proxy in maven dependency plugin folder
example:
openapi2apigee generateApi PkgTypeByQty-1 -s C:\Users\Chandra_Gaddam\Desktop\PackageTypeByQuantity.json -d C:\Users\Chandra_Gaddam\Desktop\vsCode\digiKeyApi\src\gateway
   
--------------------------------------------------python script to add flow frags--------------------------------------------------------------------------------------
move from current directory to the directory where python script is present
cd C:\Users\Chandra_Gaddam\Desktop\Python

add flowfrags to proxyendpoint default faultrule
python xmlHelper.py -f <xml_element_to_find> -r <xml_element_to_replace>  {location of the proxy default.xml file} 
example:
python xmlHelper.py -f ProxyEndpoint/DefaultFaultRule -r C:\Users\Chandra_Gaddam\Desktop\Python\DefaultFaultRule.xml  C:\Users\Chandra_Gaddam\Desktop\vsCode\digiKeyApi\src\gateway\PkgTypeByQty-1\apiproxy\proxies\default.xml 
   
python xmlHelper.py -f ProxyEndpoint/PreFlow/Request -r C:\Users\Chandra_Gaddam\Desktop\Python\PreFlowRequest.xml  C:\Users\Chandra_Gaddam\Desktop\vsCode\digiKeyApi\src\gateway\PkgTypeByQty-1\apiproxy\proxies\default.xml 
   
python xmlHelper.py -f ProxyEndpoint/PostFlow/Response -r C:\Users\Chandra_Gaddam\Desktop\Python\PostFlowResponse.xml  C:\Users\Chandra_Gaddam\Desktop\vsCode\digiKeyApi\src\gateway\PkgTypeByQty-1\apiproxy\proxies\default.xml 
   
python xmlHelper.py -f ProxyEndpoint/PostClientFlow/Response -r C:\Users\Chandra_Gaddam\Desktop\Python\PostClientFlowResponse.xml  C:\Users\Chandra_Gaddam\Desktop\vsCode\digiKeyApi\src\gateway\PkgTypeByQty-1\apiproxy\proxies\default.xml 
   
python xmlHelper.py -f TargetEndpoint/FaultRules -r C:\Users\Chandra_Gaddam\Desktop\Python\TargetFaultRule.xml  C:\Users\Chandra_Gaddam\Desktop\vsCode\digiKeyApi\src\gateway\PkgTypeByQty-1\apiproxy\targets\default.xml 
   
python xmlHelper.py -f ProxyEndpoint/Flows -a C:\Users\Chandra_Gaddam\Desktop\Python\UnknownResourcePath.xml last C:\Users\Chandra_Gaddam\Desktop\vsCode\digiKeyApi\src\gateway\PkgTypeByQty-1\apiproxy\proxies\default.xml 
   
   
----------------------------------------add mandatory policies to proxy and deploy to apigee----------------------------------------------------------------------------
change to maven dependency folder  where the proxy is created
cd C:\Users\Chandra_Gaddam\Desktop\vsCode\digiKeyApi\src\gateway\PkgTypeByQty-1


mvn apigee-enterprise:deploy -X  -P{environment} -Dusername={username} -Dpassword={password} -Dorg={organization name}
 
