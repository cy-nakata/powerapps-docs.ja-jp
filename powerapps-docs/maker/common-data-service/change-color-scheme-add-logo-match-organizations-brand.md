---
title: 組織のブランドに合わせて配色を変更またはロゴを追加 | MicrosoftDocs
ms.custom: ''
ms.date: 06/18/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
author: Mattp123
ms.assetid: 21a166a0-d25e-4260-a1e4-2ddc528787c2
caps.latest.revision: 17
ms.author: matp
manager: kvivek
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---
# <a name="create-a-theme"></a>テーマの作成

カスタマイズされていないシステムで提供される既定の色と視覚要素を変更して、自分のアプリに合わせて、ユーザー定義の外観 (テーマ) を作成することができます。 たとえば、会社ロゴを追加し、エンティティ固有の色を指定することによって、個人用の製品ブランドを作成できます。 テーマの作成には、ユーザー インターフェイスのカスタマイズ ツールを使用します。開発者はコードを記述する必要はありません。 組織で使用されるテーマを作成、変更、または削除できます。 テーマのカスタマイズは、Dynamics 365 for Outlook の Web フォームでサポートされます。 複数のテーマを定義できますが、既定のテーマとして設定して公開できるのは 1 つだけです。  
  
<a name="UseThemes"></a>   
## <a name="use-themes-to-enhance-the-user-interface-and-create-your-product-branding"></a>ユーザー インターフェイスの機能の強化と製品ブランドの作成にテーマを使用  
 テーマに合わせた構成は、アプリのユーザー インターフェイスを大幅に変えるだけでなく、その機能を強化します。 テーマ色はアプリケーション全体に適用されます。 たとえば、UI の次の視覚要素の機能を強化できます。  
  
-   製品ロゴとナビゲーション色を変更して製品ブランドを作成  
  
-   カーソルを置いたときの色や選択色など、強調色を調整  
  
-   エンティティ固有の着色を指定  
    
-   ロゴ  
  
-   ロゴ ツールヒント  
  
-   ナビゲーション バーの色  
  
-   ナビゲーション バーのシェルフの色

-   統一インターフェイスのメイン コマンド バーの色
  
-   ヘッダーの色  
  
-   グローバル リンクの色  
  
-   選択されたリンクの効果  
  
-   カーソルを置いたリンクの効果  
  
-   プロセス コントロールの色  
  
-   エンティティの既定の色  
  
-   ユーザー定義エンティティの既定の色  
  
-   コントロールの影  
  
-   コントロールの境界線  
  
<a name="Solution"></a>   
## <a name="solution-awareness"></a>ソリューション対応  
 テーマはソリューション対応ではありません。 組織のテーマに対する変更は、組織からエクスポートされるソリューションには含まれません。 データはテーマ エンティティに格納されます。このエンティティをエクスポートして、他の環境に再インポートすることができます。 インポートしたテーマが有効になるには、公開する必要があります。  
  
<a name="CloneAlter"></a>   
## <a name="copy-and-alter-the-existing-theme"></a>既存のテーマのコピーと変更  
 新しいをテーマ作成する最も簡単で最も早い方法は、既存のテーマを複製し、それを変更した後、それを保存、プレビュー、公開することです。 
 
1.  [PowerApps](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) にサインインします。

2.  **モデル駆動型** (左下) を選択します。 

3.  選択 ![設定アイコン](../model-driven-apps/media/powerapps-gear.png) (右上) > **高度なカスタマイズ**。 

4. **テーマ** で **すべてのテーマ**を選択します。 

5. **CRM の既定のテーマ**を選択します。 

次のスクリーンショットは、既定のテーマのセットアップの一部を示しています。  
  
![既定のテーマ](media/default-theme.png) 
  
 既定のテーマを複製し、色を変更しました。 次のスクリーンショットは、ナビゲーションとハイライトのための新しい色を示しています。 また、製品の新しいロゴを選択することもできます。  
  
 次のスクリーンショットは、新しいナビゲーションの色を示しています。  
  
 ![穏やかな緑のテーマ色](media/theme-gentle-green.png "穏やかな緑のテーマ色")  
  
 次のスクリーンショットは、新しいハイライト色の取引先企業エンティティ グリッドを示しています。  
  
 ![穏やかな緑色のテーマの取引先企業グリッド](media/themes-gentle-green-account-grid.png "穏やかな緑色のテーマの取引先企業グリッド")  
  
<a name="Publish"></a>   
## <a name="preview-and-publish-a-theme"></a>テーマのプレビューと公開  
 テーマをプレビューして公開するには、次の手順を実行します。  
  
-   新しいテーマを最初から作成するか、または既存のテーマを複製します。  
  
-   コマンド バーで、**プレビュー**を選択して、新しいテーマをプレビューします。 プレビュー モードを終了するには、**プレビュー**ボタンの横にある、コマンド バーの**プレビューの終了**を選択します。  
  
-   テーマを公開します。 コマンド バーで、**テーマの公開**を選択します。  
  
 次のスクリーンショットは、プレビューおよび公開のための、コマンド バーのボタンを表示しています。  
  
 ![プレビュー ボタンを使用してプレビュー モードの開始/終了](media/themes-preview-buttons.PNG "プレビュー ボタンを使用してプレビュー モードの開始/終了")  
  
<a name="BestPracticies"></a>   
## <a name="best-practices"></a>ベスト プラクティス  
 以下は、テーマのコントラスト設計と色の選択に関する推奨事項です。  
  
### <a name="theme-contrast"></a>テーマのコントラスト  
 対比色を提供する次の方法をお勧めします。  
  
-   対比色を慎重に選択します。 アプリ用 Common Data Service の標準の既定テーマでは、最適な使いやすさを確保する適切なコントラスト比を用いています。 新しいテーマに対して同様の比を使用してください。  
  
-   ハイ コントラスト モードの場合は、既定の設定を使用します。  
  
### <a name="theme-colors"></a>テーマ色  
 複数の異なる色を使用しないことをお勧めします。 エンティティごとに異なる色を設定できますが、次の 2 つのパターンのいずれかをお勧めします。  
  
-   すべてのエンティティを中間色で表現し、重要なエンティティをハイライトします。  
  
-   キューおよびキュー アイテムなどの似たエンティティまたは関連エンティティ、あるいは製品カタログ エンティティに対して同じ色を使用します。 グループの総数を少なくします。  
  
<a name="Considerations"></a>   
## <a name="custom-theme-considerations"></a>ユーザー定義のテーマに関する考慮事項  
 ユーザー定義のテーマの使用を計画するとき、次のことを考慮する必要があります:  
  
-   更新されたほとんどのユーザー インターフェイス (UI) 領域は、ユーザー定義の色で表示されます。  
  
-   テーマ色はアプリケーション全体にグローバルに適用されますが、グラデーション ボタンなどの一部の従来の UI の領域は既定の色に維持します。  
  
-   特定の領域には、既定のアイコンの色と対比するために、濃い色または薄い色を使用します。 アイコンの色はカスタマイズできません。  
  
-   エンティティは、別のサイトマップ ノードでは、さまざまな色で表示できません。  
  
-   サイトマップ ノードの色はカスタマイズできません。  
  
## <a name="see-also"></a>関連項目  
         
 [ビデオ: Dynamics 365 Customer Engagement のテーマ](http://go.microsoft.com/fwlink/p/?LinkId=529568) [組織テーマをクエリして編集](https://docs.microsoft.com/dynamics365/customer-engagement/developer/customize-dev/query-and-edit-an-organization-theme)
