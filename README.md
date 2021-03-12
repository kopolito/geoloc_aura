# Geolocation

Géolocalisation avec Salesforce

#################################

## Create a scratch org with the alias GeoAppScratch

`sfdx force:org:create -s -f config/project-scratch-def.json -a GeoAppScratch`

## creation des données de départ

### Create the Marriott Marquis account.

`sfdx force:data:record:create -s Account -v "Name='Marriott Marquis' BillingStreet='780 Mission St' BillingCity='San Francisco' BillingState='CA' BillingPostalCode='94103' Phone='(415) 896-1600' Website='www.marriott.com'"`

### Create the Hilton Union Square account

`sfdx force:data:record:create -s Account -v "Name='Hilton Union Square' BillingStreet='333 O Farrell St' BillingCity='San Francisco' BillingState='CA' BillingPostalCode='94102' Phone='(415) 771-1400' Website='www.hilton.com'"`

### Create the Hyatt account

`sfdx force:data:record:create -s Account -v "Name='Hyatt' BillingStreet='5 Embarcadero Center' BillingCity='San Francisco' BillingState='CA' BillingPostalCode='94111' Phone='(415) 788-1234' Website='www.hyatt.com'"`

In your Salesforce DX geolocation project, create a directory called data.
`mkdir data`

Export some sample data.
`sfdx force:data:tree:export -q "SELECT Name, BillingStreet, BillingCity, BillingState, BillingPostalCode, Phone, Website FROM Account WHERE BillingStreet != NULL AND BillingCity != NULL and BillingState != NULL" -d ./data`

You now have sample data that you can import in the future with this command. But don't do it now, we'll import the data into a different scratch org later.
`sfdx force:data:tree:import --sobjecttreefiles data/Account.json`

So far we’ve synchronized regular data. Now we’re going to turn to the really fun part—the code.