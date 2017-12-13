Notes about the Star Tribune instance of Driveshaft.

## Settings

There are some things that are confusing or missing from the documentation, or just suffered because Google's API system has changed a lot recently.

### Authentication for assets

This is the part of the app that downloads the spreadsheets or documents.  Driveshaft allows you to use different methods of authentication with Google, but it fails to note that the default of `GOOGLE_APICLIENT_KEY` does not actually allow a API user to download spreadsheet data unless it is viewable to everyone.

We use the `GOOGLE_APICLIENT_SERVICEACCOUNT` authentication method.

### Authentication for the application

To limit who can view the application interface, we use Google as well.

TODO: Limit by email.

### Index/list of files

The `DRIVESHAFT_SETTINGS_INDEX_KEY` setting tells Driveshaft where the list of datasets are.  Driveshaft doesn't use the data in this file directly, but reads the data from the published URL at `DRIVESHAFT_SETTINGS_INDEX_DESTINATION`

Note that you can use the interface to publish any file the API account has access to, but the index list of files helps manage things.

## Deploy

The application is currently deployed on Heroku.

### Build packs

The buildpacks that are needed for this application:

* `heroku/nodejs`
* `heroku/ruby`
