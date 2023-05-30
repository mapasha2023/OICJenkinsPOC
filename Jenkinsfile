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

sh '''

//Get Token for OIC Gen2
echo "Starting 1"
curl --location --request POST 'https://idcs-b0bf5647dbe34af4914cf420cba0294c.identity.oraclecloud.com/oauth2/v1/token'\
--header 'Content-Type: application/x-www-form-urlencoded'\
--data-urlencode 'grant_type=client_credentials'\
--data-urlencode "scope=https://59D040337868449CB0014B649FE827EC.integration.ocp.oraclecloud.com:443urn:opc:resource:consumer::all"\
--data-urlencode "client_id=6d10ff0499544a669eec7fa44c74a06f"\
--data-urlencode "client_secret=42e68606-0f44-4a7b-b13a-99e19fc27e06" --insecure -o token_OIC2.json
'''
}

}
}
}