# StartApp-Admob-Sample
Add library to gradle file

StartApp
   compile 'com.startapp:inapp-sdk:3.6.5'
   
Admob
  
    compile 'com.google.android.gms:play-services-gcm:9.8.0'
    
    compile 'com.google.android.gms:play-services-ads:9.8.0'
    
 ///////////////////////////////////////////////////////////////////////////////////////////////////////////
    private AdView adView;
    
    private InterstitialAd mInterstitialAd;
    
    private StartAppAd startApp    
    
 //////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
 
 ////////////////////// function :  showStartApp ads  zhang_code(2017-09-11)///////////////////////////////
    private void showStartApp()
    {
        startApp = new StartAppAd(this);
        
        String str = SharedPrefUtil.loadString(getBaseContext(), KeyUtils.KEY_STARTAPP_ID,"");
        
        //////////////////add startapp APP ID//////////////////////////
        
        StartAppSDK.init(this, SharedPrefUtil.loadString(getBaseContext(), KeyUtils.KEY_STARTAPP_ID,""), true);
        
        startApp.enableAutoInterstitial();
        
//        startApp.showAd(this);

//        startApp.setAutoInterstitialPreferences(new AutoInterstitialPreferences().setSecondsBetweenAds(2 * 60));


        startApp.loadAd(new AdEventListener() {
            @Override
            public void onReceiveAd(Ad ad) {
                System.out.println("Ad received");
                startApp.showAd();
            }

            @Override
            public void onFailedToReceiveAd(Ad ad) {

            }
        });
    }
    
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

  /////////////////function  : show admob for initrial style////////////////////////////////////////////////////////////////
    private  void showInitiralAdmobView()
    {
        String str = SharedPrefUtil.loadString(getBaseContext(), KeyUtils.KEY_ADMOB_INITSTIAL,"");
        mInterstitialAd = new InterstitialAd(this);

        // set the ad unit ID
        mInterstitialAd.setAdUnitId(str);

//        AdRequest adRequestInter = new AdRequest.Builder().addTestDevice(AdRequest.DEVICE_ID_EMULATOR).build();
        AdRequest adRequest = new AdRequest.Builder()
                .build();
      // Load ads into Interstitial Ads
        mInterstitialAd.loadAd(adRequest);
        
        mInterstitialAd.setAdListener(new AdListener() {
            public void onAdLoaded() {
//                showInterstitial();
                mInterstitialAd.show();
            }
            @Override
            public void onAdFailedToLoad(int i) {
                super.onAdFailedToLoad(i);
            }

        });
    }
//////////////////////////////////////////////////////admob banner//////////////////////////////////////////////////////
    private void showAdmobView()
    {
//        String admob_id = SharedPrefUtil.loadString(getBaseContext(),KeyUtils.KEY_ADMOB_ID,"");

        // admob
        String str = SharedPrefUtil.loadString(getBaseContext(), KeyUtils.KEY_ADMOB_ID,"");
        if (!str.equals(""))
        {
            // Look up the AdView as a resource and load a request.
            AdView adView1 = new AdView(this);
            adView1.setAdSize(AdSize.BANNER);
            adView1.setAdUnitId(SharedPrefUtil.loadString(getBaseContext(),KeyUtils.KEY_ADMOB_ID,""));
            admob_layout.addView(adView1);
            AdRequest adRequest = new AdRequest.Builder().build();
            adView1.loadAd(adRequest);

        } else {
//            AdView adView1 = (AdView) findViewById(R.id.adView);
//            adView1.setVisibility(View.GONE);
        }
    }
