---
title: キャンバス アプリへのデータ接続の追加 | Microsoft Docs
description: 既存のキャンバス アプリや空のアプリにデータ接続を追加できます
author: lancedMicrosoft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: anneta
ms.date: 04/06/2018
ms.author: lanced
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 33ca717967989a202fabbf8281b93f8b8263b79d
ms.sourcegitcommit: 429b83aaa5a91d5868e1fbc169bed1bac0c709ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2018
ms.locfileid: "42853206"
---
# <a name="add-a-data-connection-to-a-canvas-app-in-powerapps"></a>PowerApps でキャンバス アプリにデータ接続を追加する

PowerApps で、既存のキャンバス アプリまたはゼロから作成するアプリにデータ接続を追加します。 アプリは、SharePoint、Salesforce、OneDrive、または[他の多くのデータ ソース](connections-list.md)に接続できます。

この記事の後に来る[次のステップ](#next-steps)は、以下に示す例のように、接続したデータ ソースのデータをアプリで表示および管理することです。

* OneDrive に接続し、アプリ内で Excel ブックのデータを管理する。
* Twilio に接続し、アプリから SMS メッセージを送信する。
* SQL Server に接続し、アプリからテーブルを更新する。

## <a name="prerequisites"></a>前提条件

PowerApps に[サインアップ](../signup-for-powerapps.md)し、サインアップに使用したのと同じ資格情報を入力して[サインイン](http://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)します。

## <a name="add-a-data-source"></a>データ ソースの追加
1. **[ホーム]** タブで **[空白から開始]** タイルにポインターを合わせ、**[このアプリの作成]** を選択します。

    ![アプリを最初から作成する](./media/add-data-connection/blank-app-tile.png)

1. **[PowerApps Studio へようこそ]** ダイアログ ボックスが表示されたら、**[スキップ]** を選択します。

3. 中央のウィンドウで、**[データに接続]** をクリックまたはタップします。

4. 使用する接続が **[データ]** ウィンドウの接続の一覧に表示されている場合は、その接続を選択してアプリに追加します。 それ以外の場合、次のステップに進んでください。

    ![データ ソースの追加](./media/add-data-connection/choose-existing-connections.png)

5. **[新しい接続]** を選択して、コネクタの一覧を表示します。

    ![接続の追加](./media/add-data-connection/new-connection.png)

6. 作成する接続の種類 (たとえば、**Office 365 Outlook**) が表示されるまでコネクタの一覧をスクロールし、それを選択します。

    ![接続の選択](./media/add-data-connection/choose-connection.png)

7. **[作成]** を選択して、接続の作成とアプリへの追加の両方を行います。

    **Office 365 Outlook** などのコネクタでは、追加の手順を実行しなくても、すぐにデータを表示できます。 コネクタによっては、資格情報の入力や、特定のデータ セットの指定などの手順が要求されることがあります。 たとえば、[SharePoint](connections/connection-sharepoint-online.md) と [SQL Server](connections/connection-azure-sqldatabase.md) では、使用する前に追加情報の入力を求められます。

## <a name="add-another-data-source"></a>別のデータ ソースを追加する
1. データ ソースに追加したいコントロールを追加します。

    コントロールには、ギャラリーやリストボックスのように **Items** プロパティ、またはフォームのように **Item** プロパティが必要です。

1. (自動的に開く) **[データ]** ウィンドウで、**[データ ソース]** の一覧を開き、**[データ ソースの追加]** を選択します。

1. 手順 4 以降の手順を実行します。

## <a name="identify-or-change-a-data-source"></a>データ ソースの特定または変更
アプリを更新する際、ギャラリー、フォーム、または別のコントロールに表示されるデータ ソースを特定または変更する必要があることがあります。 たとえば、他のユーザーが作成したアプリや、以前作成したアプリを更新するときなどに、データ ソースを特定する必要があります。

1. データ ソースを特定または変更するコントロールを選択します。

    たとえば、左端付近にある画面およびコントロールの階層一覧内のギャラリーをクリックまたはタップして、(ギャラリー内のコントロールではなく) ギャラリーを選択します。

    右側のウィンドウの **[プロパティ]** タブにデータ ソース名が表示されます。

2. 変更するデータ ソースを選択するか、そのデータ ソースに関する詳細情報を表示します。

    ![データ ウィンドウ](./media/add-data-connection/data-pane.png)

3. データ ソースを変更するには、データ ソースの一覧を開き、別のソースを選択または作成します。

     ![データ ウィンドウ](./media/add-data-connection/datasource-list.png)

## <a name="next-steps"></a>次の手順
* Excel、SharePoint、SQL Server などのソースにあるデータを表示および更新するには、[ギャラリーを追加](add-gallery.md)して、[フォームを追加](add-form.md)します。
* [Office 365 Outlook](connections/connection-office365-outlook.md)、[Twitter](connections/connection-twitter.md)、[Microsoft Translator](connections/connection-microsoft-translator.md) などのソースの場合は、各コネクタに用意された機能を使用して表示や更新を行います。
