# TLSSocketFactory
TLSSocketFacory is TLS1.2 (HTTPS connection) capable with Java6 powered by BouncyCastle

## License
MIT X11 License

## How to use

URLConnection
* normal  
`HttpsURLConnection.setDefaultSSLSocketFactory(new TLSSocketFactory());`

* self-signed certificate connectable  
`HttpsURLConnection.setDefaultSSLSocketFactory(new TLSSocketFactory(true));`

* configure socket timeout (millisec: default=0)  
`HttpsURLConnection.setDefaultSSLSocketFactory(new TLSSocketFactory(true, 60000));`  

HttpClient(4.5)
``` 
private static final RequestConfig requestConfig = RequestConfig.custom()
            .setConnectTimeout(3000)
            .setSocketTimeout(10000)
            .build();

private static final SSLConnectionSocketFactory sf = new SSLConnectionSocketFactory(new TLSSocketFactory(), new String[]{"TLSv1.2"}, null, new HostnameVerifier() {
	@Override
	public boolean verify(String s, SSLSession sslSession) {
	    return true;
	}
});

private static final HttpClient httpClient = HttpClients.custom()
    .setSSLSocketFactory(sf)
    .setUserTokenHandler(NoopUserTokenHandler.INSTANCE)
    .setDefaultRequestConfig(requestConfig)
    .build();
``` 


## BouncyCastle maven repository
		<!-- https://mvnrepository.com/artifact/org.bouncycastle/bcprov-debug-jdk15on -->
		<dependency>
			<groupId>org.bouncycastle</groupId>
			<artifactId>bcprov-debug-jdk15on</artifactId>
			<version>1.55</version>
		</dependency>
		<!-- https://mvnrepository.com/artifact/org.bouncycastle/bcpkix-jdk15on -->
		<dependency>
			<groupId>org.bouncycastle</groupId>
			<artifactId>bcpkix-jdk15on</artifactId>
			<version>1.55</version>
		</dependency>
