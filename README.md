NetworkAccessManager
====================

This single header library "modernizes" QNetworkAccessManager by
adding modern C++ features to it.

An understanding of how QNetworkAccessManager works is required because
this library is a thin wrapper to it.

Example below shows an example of how to process a network response asynchronously
using a lambda.

The return argument of the API can be used to set fine tune the network request.

```
void foo::bar()
{
	QNetworkRequest networRequest( QUrl( "https://example.com" ) ) ;

	networRequest.setRawHeader( "Host","example.com" ) ;
	networRequest.setRawHeader( "Accept-Encoding","text/plain" ) ;

	QNetworkReply * e = m_network.get( networRequest,[]( QNetworkReply& e ){

		/*
		 *
		 * Process network response
		 *
		 */
	} ) ;
}

```

QNetworkAccessManager "biggest missing API" is a lack of time out API. Sometimes network requests
just disappear when they are made while on shaky network connections. This library offers a timeout API
and it can be used as follows:

```
void foo::bar()
{
	QNetworkRequest networRequest( QUrl( "https://example.com" ) ) ;

	networRequest.setRawHeader( "Host","example.com" ) ;
	networRequest.setRawHeader( "Accept-Encoding","text/plain" ) ;

	QNetworkReply * e = m_network.get( networRequest,[]( QNetworkReply& e ){

		/*
		 *
		 * Process network response
		 *
		 */

	} ) ;

	int timeOutInSeconds = 10 ;

	m_network.timeOutManager( timeOutInSeconds,e,[](){

		/*
		 *
		 * Handle time out here
		 *
		 */
	} ) ;
}

```
