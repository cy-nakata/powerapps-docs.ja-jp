---
title: キャンバス アプリを共有する | Microsoft Docs
description: キャンバス アプリを実行または修正するためのアクセス許可を他のユーザーに付与することで、キャンバス アプリを共有します。
author: AFTOwen
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: ''
ms.date: 07/11/2018
ms.author: anneta
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 926d2b4b0d24f07a9a4cd42216e7d737db57308c
ms.sourcegitcommit: 429b83aaa5a91d5868e1fbc169bed1bac0c709ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2018
ms.locfileid: "42853844"
---
# <a name="share-a-canvas-app-in-powerapps"></a>PowerApps でのキャンバス アプリの共有

ビジネス ニーズに対応するキャンバス アプリをビルドした後、アプリを実行できる組織内のユーザー、およびアプリを変更したり、再度共有したりすることもできるユーザーを指定します。 各ユーザーを名前で指定するか、Azure Active Directory のセキュリティ グループを指定します。 すべてのユーザーがアプリから恩恵を受ける場合、組織全体がアプリを実行できるように指定します。

> [!IMPORTANT]
> 期待どおり機能する共有アプリの場合、アプリの基になるデータ ソース ([Common Data Service for Apps](#common-data-service-for-apps)、[Excel](share-app-data.md) など) のアクセス許可を管理する必要もあります。 アプリが依存する[その他のリソース](share-app-resources.md) (フロー、ゲートウェイ、接続など) を共有する必要がある場合もあります。

## <a name="prerequisites"></a>前提条件

アプリを共有するには、そのアプリを (ローカルではなく) クラウドに保存して、アプリを発行する必要があります。

- ユーザーがアプリで行う内容を理解し、リストで簡単に見つけられるように、アプリにわかりやすい名前と明確な説明を追加します。 PowerApps Studio の **[ファイル]** メニューで、**[アプリの設定]** を選択し、説明を入力するか貼り付けます。

- 変更を加えるたびに、他のユーザーがそれらの変更を表示する必要がある場合は、再度アプリを保存および発行する必要があります。

## <a name="share-an-app"></a>アプリを共有する

1. PowerApps に[サインイン](https://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)し、左端近くにある **[アプリ]** を選びます。

    ![アプリの一覧を表示する](./media/share-app/file-apps.png)

1. 共有するアプリの省略記号 (...) を選択し、**[共有]** を選択します。

    ![共有画面を開く](./media/share-app/ellipsis-share.png)

1. アプリを共有する Azure Active Directory のユーザーまたはセキュリティ グループで指定します。

    > [!NOTE]
    > 組織内の配布グループ、または組織外のユーザーまたはグループとアプリを共有することはできません。

    ![ユーザーを指定する](./media/share-app/share-list.png)

    アプリを実行できるように組織全体とアプリを共有することもできますが、そのようにして共有を受けたユーザーはアプリを変更したり他のユーザーと共有したりすることはできません。

1. (省略可能) ユーザーがアプリを見つけられるように、電子メールの招待状を送信するチェック ボックスを選択します。

    招待状には、ユーザーがアプリを実行できるリンクが含まれています。

    - ユーザーがデスクトップ コンピューター上のリンクを選択すると、アプリが [Dynamics 365](http://home.dynamics.com) で表示されます。
    - ユーザーがモバイル デバイス上のリンクを選択すると、アプリは PowerApps モバイルで表示されます。

    ユーザーにアプリを変更するアクセス許可を付与する場合、メッセージには PowerApps Studio で編集するためにアプリを開くための別のリンクも含まれます。

    招待状を送信しているかどうかに関係なく、ユーザーは [Dynamics 365](http://home.dynamics.com) 上の AppSource からアプリを実行できます。 **[編集可能]** アクセス許可があるユーザーは、[PowerApps](http://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) 内からアプリを編集することもできます。

1. ユーザーまたはセキュリティ グループごとにアクセス許可を指定して、**[保存]** を選択します。

    - **使用可能**: ユーザーはアプリを実行できますが、共有することはできません。
    - **編集可能**: ユーザーはアプリを実行したり、カスタマイズしたり、カスタマイズしたバージョンを他のユーザーと共有したりすることができます。

        ![アクセス許可を指定する](./media/share-app/edit-use.png)

    ユーザーまたはセキュリティ グループのアクセス許可を変更するには、ユーザーまたはグループに既にあるアクセス許可の横にある下向き矢印を選択して、別のアクセス許可を指定します。

    ユーザーまたはグループのすべてのアクセス許可を削除するには、そのユーザーまたはグループについて、**[x]** アイコンを選択します。

## <a name="security-group-considerations"></a>セキュリティ グループに関する考慮事項

- セキュリティ グループでアプリを共有すると、そのグループの既存のメンバーとグループに参加するユーザーは、そのグループに指定したアクセス許可が付与されます。 アクセス権がある別のグループに属しているか、個人としてアクセス許可を付与しない限り、グループから脱退する任意のユーザーはそのアクセス許可を失います。
- セキュリティ グループのすべてのメンバーは、アプリに関して、グループ全体と同じアクセス許可を持ちます。 ただし、そのグループの 1 人以上のメンバーに対してより多くのアクセス許可を指定することで、メンバーのアクセス許可を増やすことができます。 たとえば、セキュリティ グループ A に**使用可能**アクセス許可を付与し、そのグループに属するユーザー B には**編集可能**アクセス許可を付与することができます。 セキュリティ グループのすべてのメンバーはアプリを実行できますが、ユーザー B だけは編集することができます。 セキュリティ グループ A に**編集可能**アクセス許可を付与し、ユーザー B に**使用可能**アクセス許可を付与した場合は、ユーザー B はアプリを編集できます。

## <a name="manage-entity-permissions"></a>エンティティのアクセス許可を管理する

### <a name="common-data-service-for-apps"></a>Common Data Service for Apps

Common Data Service (CDS) for Apps に基づいてアプリを作成する場合は、そのアプリを稼働させるユーザーが、アプリが依存するその 1 つまたは複数のエンティティに対して適切なアクセス許可を確実に持つようにする必要もあります。 具体的には、それらのユーザーは、関連するレコードの作成、閲覧、作成、削除など、タスクを実行できるセキュリティ ロールに属している必要があります。 多くの場合は、ユーザーがアプリを使用するときに必要である厳密なアクセス許可によって 1 つまたは複数のカスタム セキュリティ ロールを作成します。 その後、その 1 つまたは複数のロールを必要に応じてユーザーに割り当てることができます。 

#### <a name="prerequisite"></a>前提条件

次の 2 つの手順を行うには、CDS for Apps データベース用の**システム管理者**アクセス許可を用意する必要があります。

#### <a name="create-a-security-role"></a>セキュリティ ロールを作成する

1. [PowerApps にサインイン](https://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)して、共有するアプリと同じ環境にいることを確認します。

1. 右上隅の歯車アイコンを選択して、**[高度なカスタマイズ]** を選択します。

    ![[高度なカスタマイズ] ウィンドウを開く](media/share-app/advanced-customizations.png)

1. **セキュリティ ロール** リンクを選択します。

    ![セキュリティ ロールを開く](media/share-app/security-roles.png)

1. **[すべてのロール]** の下で **[新規]** を選択し、作成しているロールの名前を入力するか貼り付けます。

    ![セキュリティ ロールを作成する](media/share-app/new-role.png)

1. アプリが使用するエンティティを見つけるために 1 つまたは複数のタブを選択して、セキュリティ ロールを付与するアクセス許可を選択します。

    たとえば、このグラフィックは、セキュリティ ロールがアカウント エンティティのレコードを作成、閲覧、作成、削除することができることを示します。これは、**[コア レコード]** タブに表示されます。

    ![アクセス許可を指定する](media/share-app/grant-access.png)

1. **[保存して閉じる]** を選びます。

#### <a name="assign-a-user-to-a-role"></a>ロールへのユーザーの割り当て

1. 前の手順で示されたように、**[高度なカスタマイズ]** ウィンドウを開いて、**[ユーザー]** リンクを選択します。

    ![[ユーザー] リンク](media/share-app/open-users.png)

1. 右上隅で、ロールに割り当てる必要があるユーザーの名前を入力または貼り付けて、検索アイコンを選択します。

    ![ユーザーを検索する](media/share-app/search-users.png)

1. 検索結果で、必要な結果をポイントして、表示されるチェック ボックスを選択します。

1. 上部のバナーで、**[ロールの管理]** を選択します。

1. 表示されるダイアログ ボックスで、**[Common Data Service ユーザー]** および自分のアプリに必要なロール ユーザーのチェック ボックスを選択して、**[OK]** を選択します。

    ![ロールへのユーザーの割り当て](media/share-app/assign-users.png)

### <a name="common-data-service-previous-version"></a>Common Data Service (以前のバージョン)

古いバージョンの Common Data Service に基づくアプリを共有するときは、サービスに対する実行時のアクセス許可を別途共有する必要があります。 そのためのアクセス許可がない場合は、ご利用の環境の管理者に問い合わせてください。
