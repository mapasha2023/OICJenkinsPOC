pipeline
{
agent any
stages
{
stage('Generate Token')
{
steps
{
bat '''
curl -s "https://idcs-b0bf5647dbe34af4914cf420cba0294c.identity.oraclecloud.com/oauth2/v1/token" \
--header "Authorization: Basic NmQxMGZmMDQ5OTU0NGE2NjllZWM3ZmE0NGM3NGEwNmY6NDJlNjg2MDYtMGY0NC00YTdiLWIxM2EtOTllMTlmYzI3ZTA2" \
--header "Content-Type: application/x-www-form-urlencoded" \
--data-urlencode "grant_type=client_credentials" \
--data-urlencode "scope=https://59D040337868449CB0014B649FE827EC.integration.ocp.oraclecloud.com:443urn:opc:resource:consumer::all" \
--data-urlencode "client_id=6d10ff0499544a669eec7fa44c74a06f" \
--data-urlencode 'client_secret=42e68606-0f44-4a7b-b13a-99e19fc27e06' --insecure -o token_OIC3.json
'''
}
}
stage('Deployment of IAR Files to OIC') 
{
steps
{
bat '''
curl --location "https://testinstance-idevjxz332qf-ia.integration.ocp.oraclecloud.com/ic/api/integration/v1/integrations/archive" --header "Authorization: Basic cG9jdXNlcjpIVk9JQ01heSMyMDIz" --form "file=@"BIREPORT_CS_01.00.0000.iar"
'''
}
}
stage('Activate the Integration')
{
steps
{
bat '''
curl --header "Authorization: Basic cG9jdXNlcjpIVk9JQ01heSMyMDIz" --header "X-HTTP-Method-Override:PATCH" --header "Content-Type:application/json" -d @soapconnprop.json https://testinstance-idevjxz332qf-ia.integration.ocp.oraclecloud.com/ic/api/integration/v1/connections/SOAPCON_CS
curl --header "Authorization: Basic cG9jdXNlcjpIVk9JQ01heSMyMDIz" --header "X-HTTP-Method-Override:PATCH" --header "Content-Type:application/json" -d @restconnprop.json https://testinstance-idevjxz332qf-ia.integration.ocp.oraclecloud.com/ic/api/integration/v1/connections/RESTCON_CS
curl --header "Authorization: Basic cG9jdXNlcjpIVk9JQ01heSMyMDIz" --header "X-HTTP-Method-Override:PATCH" --header "Content-Type:application/json" -d @ftpconnprop.json https://testinstance-idevjxz332qf-ia.integration.ocp.oraclecloud.com/ic/api/integration/v1/connections/FTPCONN_CHANDANA
curl --location --request PUT --header "Authorization: Basic ZGV2b3BzX3VzZXI6T2ljX0plbmtpbnMjMjAyMw==" --header "Content-Type:application/json" -d  @lookup.json https://testinstance-idevjxz332qf-ia.integration.ocp.oraclecloud.com/ic/api/integration/v1/lookups/BIReport_CS
curl --header "Authorization: Basic cG9jdXNlcjpIVk9JQ01heSMyMDIz" --header "Content-Type:application/json" --header "X-HTTP-Method-Override:PATCH" -d @update.json curl --location "https://testinstance-idevjxz332qf-ia.integration.ocp.oraclecloud.com/ic/api/integration/v1/integrations/BIREPORT_CS|01.00.0000"
'''
}
}
}
}
