pipeline
{
agent any
// environment
// {
// token_type = "Bearer"
// }
stages
{
stage('Deployment') 
{
steps
{
curl --location "https://testinstance-idevjxz332qf-ia.integration.ocp.oraclecloud.com/ic/api/integration/v1/integrations/archive" --header "Authorization: Basic cG9jdXNlcjpIVk9JQ01heSMyMDIz" --form "file=@"BIREPORT_CS_01.00.0000.iar"
}
}
}
}
