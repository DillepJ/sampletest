# sampletest
Testing

public void checkLoginScreen() {
        /*loginScreenBinding.username.setText("testdemo"); //loc village level
        loginScreenBinding.password.setText("test123#$");*/
        loginScreenBinding.username.setText("kpmanghab1"); //loc-hab level
        loginScreenBinding.password.setText("test123#$");
        /*loginScreenBinding.username.setText("aritmnrvp25u2"); //prod
        loginScreenBinding.password.setText("rdas566#$");*/
        /*loginScreenBinding.username.setText("mdumduevp34u2"); //prod
        loginScreenBinding.password.setText("rdas673#$");*/
        /*loginScreenBinding.username.setText("tvrtrvrvp3u2"); //prod
        loginScreenBinding.password.setText("rdas600#$");*/
        /*loginScreenBinding.username.setText("nmknpetvp10u3"); //prod
        loginScreenBinding.password.setText("rdas481#$");*/
        final String username = loginScreenBinding.username.getText().toString().trim();
        final String password = loginScreenBinding.password.getText().toString().trim();
        prefManager.setUserPassword(password);

        if (Utils.isOnline()) {
            if (!validate())
                return;
            else if (prefManager.getUserName().length() > 0 && password.length() > 0) {
                new ApiService(this).makeRequest("LoginScreen", Api.Method.POST, UrlGenerator.getLoginUrl(), loginParams(), "not cache", this);
            } else {
                Utils.showAlert(this, getResources().getString(R.string.please_enter_the_user_name_and_password));
            }
        } else {
            //Utils.showAlert(this, getResources().getString(R.string.no_internet));
            AlertDialog.Builder ab = new AlertDialog.Builder(
                    LoginScreen.this);
            ab.setMessage(getResources().getString(R.string.please_turn_on_network_or_continue_offline));
            ab.setPositiveButton(getResources().getString(R.string.settings),
                    new DialogInterface.OnClickListener() {
                        public void onClick(DialogInterface dialog,
                                            int whichButton) {
                            Intent I = new Intent(
                                    android.provider.Settings.ACTION_WIRELESS_SETTINGS);
                            startActivity(I);
                        }
                    });
            ab.setNegativeButton(getResources().getString(R.string.continue_with_off_line),
                    new DialogInterface.OnClickListener() {
                        public void onClick(DialogInterface dialog,
                                            int whichButton) {
                            offline_mode(username, password);
                        }
                    });
            ab.show();
        }
    }
