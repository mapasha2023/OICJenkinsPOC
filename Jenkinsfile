pipeline
{
agent any
environment
{
token_type = "Bearer"
}

stages
{
stage('GetBearerToken')
{
steps
{
withCredentials([usernamePassword(credentialsId: "devops_user", passwordVariable: "42e68606-0f44-4a7b-b13a-99e19fc27e06", usernameVariable: "6d10ff0499544a669eec7fa44c74a06f")])
{
sh '''

//Get Token for OIC Gen2
curl --location --request POST 'https://idcs-b0bf5647dbe34af4914cf420cba0294c.identity.oraclecloud.com/oauth2/v1/token'\
--header 'Content-Type: application/x-www-form-urlencoded'\
--data-urlencode 'grant_type=client_credentials'\
--data-urlencode "scope=https://59D040337868449CB0014B649FE827EC.integration.ocp.oraclecloud.com:443urn:opc:resource:consumer::all"\
--data-urlencode "client_id=$clientId"\
--data-urlencode "client_secret=$clientsecret" --insecure -o token_OIC2.json
'''
}
}
}

stage('Deploy Integration')
{
steps
{
sh '''
BEARER_TOKEN_OIC3=$( jq -r '.access_token' token_OIC2.json )


//Importing to Gen3
curl -X POST -v -k --insecure --location-trusted -F "file=@$BIREPORT_CS_01.00.0000.iar" -F 'type=application/octet-stream' 'https://design.integration.us-ashburn.ocp.oraclecloud.com/ic/api/integration/v1/integrations/archive?integrationInstance=TestInstance' --ssl-no-revoke --header "Authorization: $token_type$BEARER_TOKEN"
//{Service Instance} you can find in OIC3 home paage.
'''
}
}
}
}