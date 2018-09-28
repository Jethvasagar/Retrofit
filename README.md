# Retrofit

 implementation 'com.google.code.gson:gson:2.8.2'
    implementation 'com.squareup.retrofit2:retrofit:2.4.0'
    implementation 'com.squareup.retrofit2:converter-gson:2.4.0'
    implementation 'com.squareup.okhttp3:logging-interceptor:3.9.1'
    
    
    
    public class APIClient {

    private static Retrofit retrofit = null;

    public static APIService getApiClient(){

        if(retrofit == null){

            HttpLoggingInterceptor httpLoggingInterceptor = new HttpLoggingInterceptor();
            httpLoggingInterceptor.setLevel(HttpLoggingInterceptor.Level.BODY);
            OkHttpClient okHttpClient = new OkHttpClient.Builder()
                    .addInterceptor(httpLoggingInterceptor)
                    .connectTimeout(15, TimeUnit.SECONDS)
                    .readTimeout(15, TimeUnit.SECONDS)
                    .writeTimeout(15, TimeUnit.SECONDS).build();

            retrofit = new Retrofit.Builder()
                    .baseUrl(ApiConst.BASE_URL)
                    .client(okHttpClient)
                    .addConverterFactory(GsonConverterFactory.create())
                    .build();
        }
        return retrofit.create(APIService.class);
    }

    public APIService getInstance(){
        return retrofit.create(APIService.class);
    }
}




_____________

 APIClient.getApiClient().login(loginReq)
