---
title: 'Tutorial: Azure AD SSO integration with Datto File Protection Single Sign On'
description: Learn how to configure single sign-on between Azure Active Directory and Datto File Protection Single Sign On.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: CelesteDG
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 04/13/2022
ms.author: jeedes

---

# Tutorial: Azure AD SSO integration with Datto File Protection Single Sign On

In this tutorial, you'll learn how to integrate Datto File Protection Single Sign On with Azure Active Directory (Azure AD). When you integrate Datto File Protection Single Sign On with Azure AD, you can:

* Control in Azure AD who has access to Datto File Protection Single Sign On.
* Enable your users to be automatically signed-in to Datto File Protection Single Sign On with their Azure AD accounts.
* Manage your accounts in one central location - the Azure portal.

## Prerequisites

To get started, you need the following items:

* An Azure AD subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/free/).
* Datto File Protection Single Sign On enabled subscription.
* Along with Cloud Application Administrator, Application Administrator can also add or manage applications in Azure AD.
For more information, see [Azure built-in roles](../roles/permissions-reference.md).

## Scenario description

In this tutorial, you configure and test Azure AD SSO in a test environment.

* Datto File Protection Single Sign On supports **SP** and **IDP** initiated SSO.

## Add Datto File Protection Single Sign On from the gallery

To configure the integration of Datto File Protection Single Sign On into Azure AD, you need to add Datto File Protection Single Sign On from the gallery to your list of managed SaaS apps.

1. Sign in to the Azure portal using either a work or school account, or a personal Microsoft account.
1. On the left navigation pane, select the **Azure Active Directory** service.
1. Navigate to **Enterprise Applications** and then select **All Applications**.
1. To add new application, select **New application**.
1. In the **Add from the gallery** section, type **Datto File Protection Single Sign On** in the search box.
1. Select **Datto File Protection Single Sign On** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

## Configure and test Azure AD SSO for Datto File Protection Single Sign On

Configure and test Azure AD SSO with Datto File Protection Single Sign On using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between an Azure AD user and the related user in Datto File Protection Single Sign On.

To configure and test Azure AD SSO with Datto File Protection Single Sign On, perform the following steps:

1. **[Configure Azure AD SSO](#configure-azure-ad-sso)** - to enable your users to use this feature.
    1. **[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with B.Simon.
    1. **[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable B.Simon to use Azure AD single sign-on.
1. **[Configure Datto File Protection Single Sign On SSO](#configure-datto-file-protection-single-sign-on-sso)** - to configure the single sign-on settings on application side.
    1. **[Create Datto File Protection Single Sign On test user](#create-datto-file-protection-single-sign-on-test-user)** - to have a counterpart of B.Simon in Datto File Protection Single Sign On that is linked to the Azure AD representation of user.
1. **[Test SSO](#test-sso)** - to verify whether the configuration works.

## Configure Azure AD SSO

Follow these steps to enable Azure AD SSO in the Azure portal.

1. In the Azure portal, on the **Datto File Protection Single Sign On** application integration page, find the **Manage** section and select **single sign-on**.
1. On the **Select a single sign-on method** page, select **SAML**.
1. On the **Set up single sign-on with SAML** page, click the pencil icon for **Basic SAML Configuration** to edit the settings.

   ![Screenshot shows to edit Basic SAML Configuration.](common/edit-urls.png "Basic Configuration")

1. On the **Basic SAML Configuration** section, the user does not have to perform any step as the app is already pre-integrated with Azure.

1. On the **Basic SAML Configuration** section, if you wish to configure the application in **SP** initiated mode then perform the following steps:

    a. In the **Identifier** textbox, type the URL:
    `https://saml.fileprotection.datto.com/singlesignon/saml/metadata`

    b. In the **Reply URL** textbox, type the URL:
    `https://saml.fileprotection.datto.com/singlesignon/saml/SSO`

    c. In the **Sign on URL** textbox, type a URL using the following pattern:
    `https://<SUBDOMAIN>.fileprotection.datto.com`
    
    > [!NOTE]
	> This value is not real. Update this value with the actual Sign on URL. Contact [Datto File Protection Single Sign On Client support team](mailto:ms-sso-support@ot.soonr.com) to get this value. You can also refer to the patterns shown in the **Basic SAML Configuration** section in the Azure portal.

1. On the **Set up single sign-on with SAML** page, In the **SAML Signing Certificate** section, click copy button to copy **App Federation Metadata Url** and save it on your computer.

	![Screenshot shows the Certificate download link.](common/copy-metadataurl.png "Certificate")

### Create an Azure AD test user

In this section, you'll create a test user in the Azure portal called B.Simon.

1. From the left pane in the Azure portal, select **Azure Active Directory**, select **Users**, and then select **All users**.
1. Select **New user** at the top of the screen.
1. In the **User** properties, follow these steps:
   1. In the **Name** field, enter `B.Simon`.  
   1. In the **User name** field, enter the username@companydomain.extension. For example, `B.Simon@contoso.com`.
   1. Select the **Show password** check box, and then write down the value that's displayed in the **Password** box.
   1. Click **Create**.

### Assign the Azure AD test user

In this section, you'll enable B.Simon to use Azure single sign-on by granting access to Datto File Protection Single Sign On.

1. In the Azure portal, select **Enterprise Applications**, and then select **All applications**.
1. In the applications list, select **Datto File Protection Single Sign On**.
1. In the app's overview page, find the **Manage** section and select **Users and groups**.
1. Select **Add user**, then select **Users and groups** in the **Add Assignment** dialog.
1. In the **Users and groups** dialog, select **B.Simon** from the Users list, then click the **Select** button at the bottom of the screen.
1. If you are expecting a role to be assigned to the users, you can select it from the **Select a role** dropdown. If no role has been set up for this app, you see "Default Access" role selected.
1. In the **Add Assignment** dialog, click the **Assign** button.

## Configure Datto File Protection Single Sign On SSO

To configure single sign-on on **Datto File Protection Single Sign On** side, you need to send the **App Federation Metadata Url** to [Datto File Protection Single Sign On support team](mailto:ms-sso-support@ot.soonr.com). They set this setting to have the SAML SSO connection set properly on both sides.

### Create Datto File Protection Single Sign On test user

In this section, you create a user called Britta Simon in Datto File Protection Single Sign On. Work with [Datto File Protection Single Sign On support team](mailto:ms-sso-support@ot.soonr.com) to add the users in the Datto File Protection Single Sign On platform. Users must be created and activated before you use single sign-on.

## Test SSO 

In this section, you test your Azure AD single sign-on configuration with following options. 

#### SP initiated:

* Click on **Test this application** in Azure portal. This will redirect to Datto File Protection Single Sign On Sign on URL where you can initiate the login flow.  

* Go to Datto File Protection Single Sign On Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

* Click on **Test this application** in Azure portal and you should be automatically signed in to the Datto File Protection Single Sign On for which you set up the SSO. 

You can also use Microsoft My Apps to test the application in any mode. When you click the Datto File Protection Single Sign On tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Datto File Protection Single Sign On for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](../user-help/my-apps-portal-end-user-access.md).

## Next steps

Once you configure Datto File Protection Single Sign On you can enforce session control, which protects exfiltration and infiltration of your organization’s sensitive data in real time. Session control extends from Conditional Access. [Learn how to enforce session control with Microsoft Cloud App Security](/cloud-app-security/proxy-deployment-aad).