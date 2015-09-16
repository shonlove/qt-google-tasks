# Introduction #

The qt-google-tasks example uses Google Tasks API. To use API you need to register your own application on Google. Do not worry: the procedure is very simple.


# Details #

You need to login to Google, so first you need to create simple Google account. Then you can visit the page

**https://code.google.com/apis/console**

there you can create your application. You need to check access to **Tasks API** in tab "Services" (set Status On as shown in the next figure).

![http://dl.dropbox.com/u/72326178/SetServiceTasks.jpg](http://dl.dropbox.com/u/72326178/SetServiceTasks.jpg)

Then you need create client ID for your application as a web application (example page view for this in next figure).

![http://dl.dropbox.com/u/72326178/SetAPIAccess.jpg](http://dl.dropbox.com/u/72326178/SetAPIAccess.jpg)

**IMPORTANT!** For Redirect\_URI you should select any valid web server with any address on them.

Then  you can see credentials of your application.  You need to copy and paste **Client\_ID** and **Redirect\_URI** and **Client\_secret** to the file oauth2.cpp.
```
OAuth2::OAuth2(QWidget* parent)
{
    //You need to login to Google, so first you need to create simple
    //Google account. Then you can visit the page
    //
    // https://code.google.com/apis/console
    //
    //there you can create your application. You need to check access to Tasks API.
    //
    //Then  you can see credentials of your application.
    //You need to copy and paste Client_ID and Redirect_URI to the strings below.
    //

    m_strEndPoint = "https://accounts.google.com/o/oauth2/auth";
    m_strScope = "https://www.googleapis.com/auth/tasks"; //Access to Tasks service

    m_strClientID = "YOUR_CLIENT_ID_HERE";
    m_strClientSecret = "YOUR_CLIENT_SECRET_HERE";
    m_strRedirectURI = "YOUR_REDIRECT_URI_HERE";

    m_pLoginDialog = NULL;
    m_pParent = parent;
    m_pSettings = NULL;

    m_pNetworkAccessManager = new QNetworkAccessManager(this);
    connect(m_pNetworkAccessManager, SIGNAL(finished(QNetworkReply*)),
            this, SLOT(replyFinished(QNetworkReply*)));
}
```

Additionally you can specify your company name in the file **form.cpp**.
```
Form::Form(QWidget *parent) :
    QWidget(parent),
    ui(new Ui::Form)
{
    ui->setupUi(this);

    m_strCompanyName = "YOU_COMPANY_NAME_HERE";
    m_strAppName = "QtTasks";

    // Load settings
```

After that you can compile and run **qt-google-tasks**.