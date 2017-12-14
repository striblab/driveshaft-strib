Notes about the Star Tribune instance of Driveshaft.

## Settings

There are some things that are confusing or missing from the documentation, or just suffered because Google's API system has changed a lot recently.

### Authentication for assets

This is the part of the app that downloads the spreadsheets or documents.  Driveshaft allows you to use different methods of authentication with Google, but it fails to note that the default of `GOOGLE_APICLIENT_KEY` does not actually allow a API user to download spreadsheet data unless it is viewable to everyone.

We use the `GOOGLE_APICLIENT_SERVICEACCOUNT` authentication method.

### Authentication for the application

Unfortunately, what works locally and what works on Heroku are different.

#### Locally

Given that the `GOOGLE_APICLIENT_CLIENTSECRETS_WEB` authentication method did not work locally, use the `GOOGLE_APICLIENT_CLIENTSECRETS_INSTALLED` method instead.

#### Production

Given that the `GOOGLE_APICLIENT_CLIENTSECRETS_INSTALLED` authentication method did not work locally, use the `GOOGLE_APICLIENT_CLIENTSECRETS_WEB` method instead.

**NOTE**: Given new Google policies, a user logging in will be presented with a *"This app isn't verified"*, which is not cool, but not a trivial work around.

#### Limited to email

We have also added a feature to limit users by email address.  This list is managed in the `DRIVESHAFT_SETTINGS_AUTH_EMAILS` variable and should contain a comma separated list of emails of who can access the application.

### Index/list of files

The `DRIVESHAFT_SETTINGS_INDEX_KEY` setting tells Driveshaft where the list of datasets are.  Driveshaft doesn't use the data in this file directly, but reads the data from the published URL at `DRIVESHAFT_SETTINGS_INDEX_DESTINATION`

Note that you can use the interface to publish any file the API account has access to, but the index list of files helps manage things.

### AWS

The region setting cannot be changed per deployment or URL?  This is unfortunate because our buckets are on different regions.

## Deploy

The application is currently deployed on Heroku.

### Build packs

The buildpacks that are needed for this application:

* `heroku/nodejs`
* `heroku/ruby`
