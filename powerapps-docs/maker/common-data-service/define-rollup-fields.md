---
title: PowerApps でロールアップ フィールドを定義する | MicrosoftDocs
description: ロールアップ フィールドを定義する方法を説明します
ms.custom: ''
ms.date: 05/23/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
  - powerapps
author: Mattp123
ms.assetid: ff0504a1-01bd-4f9b-b884-7f84911d86c3
caps.latest.revision: 58
ms.author: matp
manager: kvivek
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---

# <a name="define-rollup-fields-that-aggregate-values"></a>値を集約するロールアップ フィールドを定義

ロールアップ フィールドは、主要業務指標を監視することによって、ユーザーがデータを把握するのに役立ちます。 ロールアップ フィールドには、指定したレコードに関連するレコードに対して計算された集計値が含まれています。 これには、電子メールや予定など定期的なエンティティと活動エンティティが含まれます。

より複雑なシナリオでは、レコードの階層にわたるデータを集計できます。 管理者またはカスタマイザーの場合は、PowerApps のカスタマイズ ツールを使用してコードを記述する必要なく、ロールアップ フィールドを定義できます。  
  
<a name="BKMK_benefitsandcapabilities"></a> 
 
## <a name="rollup-fields-benefits-and-capabilities"></a>ロールアップ フィールドの利点と機能  

ロールアップ フィールドの利点と機能には次のものがあります。  
  
- ビジュアル編集が簡単です。 通常のフィールドを作成する場合とまったく同じように、フィールド エディターを使用して、ロールアップ フィールドを作成できます。  
- 幅広い種類の集計機能。 `SUM`、`COUNT`、`MIN`、`MAX`、および `AVG` の関数を使用してデータを集計できます。  
- 集計に対応した十分なフィルターサポート。 複数の条件を設定すると同時に、ソース エンティティまたは関連エンティティに対して各種フィルターを設定できます。  
- ユーザー インターフェイスとのシームレスな統合。 ロールアップ フィールドをフォーム、ビュー、グラフ、レポートに組み込むことができます。  
- ロールアップ フィールドはソリューション コンポーネントです。 ロールアップ フィールドは環境間でコンポーネントとして簡単に移動し、ソリューションで配布することができます。  
- ロールアップ フィールドと計算フィールドは相互補完的です。 ロールアップ フィールドを計算フィールドの一部として、逆に、計算フィールドをロールアップ フィールドの一部として使用できます。  
- カスタム コントロールを使用するように、ロールアップ フィールドを構成できます。  
  
 ロールアップ フィールドの一部の例として、以下のものがあります。  
  
- 取引先企業のオープンしている営業案件の合計売上見込み  
- 1 つの階層内のすべての取引先企業に関してオープンしている営業案件の合計売上見込み  
- 下位の営業案件を含む営業案件の合計売上見込み  
- キャンペーンによって発生した見込みのある潜在顧客の合計売上見込み  
- 1 つの階層内のすべての取引先企業に関して高優先度のオープンしているサポート案件の数  
- 1つの取引先企業に関して高優先度のすべてのオープンしているサポート案件がもっとも早く作成された時期  
  
各ロールアップ フィールドには、*&lt;fieldname&gt;*`_date` と *&lt;fieldname&gt;*`_state` の接尾語のパターンを持つ 2 つの付属フィールドが作成されます。 `_date` フィールドは日時データを含み、`_state` フィールドは整数データが含まれます。 `_state` フィールドには次の値があります。  
  
|Value|都道府県|説明|  
|-|-|-|  
|0|NotCalculated|このフィールド値はまだ計算されていません。|  
|1|計算|このフィールド値は、_date フィールドの最新の更新時間ごとに計算されます。|  
|2|OverflowError|このフィールド値の計算によってオーバフロー エラーが発生しました。|  
|3|OtherError|このフィールド値の計算は内部エラーによって失敗しました。 計算ジョブの次の実行によって、これが修復されるみたいです。|  
|4|RetryLimitExceeded|並行処理の多さと競合のロックが原因で、値の計算の再試行の最大数を超過し、フィールド値の計算に失敗しました。|  
|5|HierarchicalRecursionLimitReached|最大限度の階層の深さに計算が到達したことが原因で、フィールド値の計算に失敗しました。|  
|6|LoopDetected|レコードの階層で再帰的ループが検出されたことが原因で、フィールド値の計算に失敗しました。|  
  
<a name="BKMK_calculations"></a>  
 
## <a name="rollup-calculations"></a>ロールアップ計算  

ロールアップは、バックグラウンドで非同期に実行される、スケジュールされたシステム ジョブによって計算されます。 ロールアップ ジョブを表示および管理する管理者になる必要があります。 

### <a name="view-rollup-jobs"></a>ロールアップ ジョブの表示

ロールアップ ジョブを表示するには:

1. **Common Data Service の既定のソリューション**を表示しながら URL を編集し、`dynamics.com` の後にすべてを削除してページを更新します。
2. **設定**領域で**システム** > **システム ジョブ**を選択します。<br />![システム ジョブに移動](media/navigate-system-jobs.png)
1. ビュー セレクターで、**定期システム ジョブ**を選択します。
2. 関連するジョブをすばやく見つけるため、システム ジョブの種類によってフィルター処理できます: **ロールアップ フィールドの一括計算**または**ロールアップ フィールドの計算**。
 
### <a name="mass-calculate-rollup-field"></a>ロールアップ フィールドの一括計算

**ロールアップ フィールドの一括計算**は、ロールアップ フィールドごとに作成された定期的なジョブです。 このジョブは、ロールアップ フィールドを作成または更新した後に 1 回実行されます。 このジョブは、このフィールドが含まれるすべての既存のレコードの指定されたロールアップ フィールドの値を再計算します。 既定では、このジョブは、フィールドの作成または更新から12時間後に実行されます。 ジョブが完了すると、このジョブは、遠い将来、約 10 年後に実行されるように自動的にスケジュールされます。 フィールドが変更されると、ジョブは更新から 12 時間後に再度実行されるように再設定されます。 環境の非稼動時間中に、**ロールアップ フィールドの一括計算**が実行されるようにするには、12 時間の遅延が確実に必要です。 ロールアップ フィールドが作成または変更された後、**ロールアップ フィールドの一括計算**ジョブが非稼働時間中に実行するように、管理者が開始時間を調整することをお勧めします。 たとえば、ロールアップ フィールドの効率的な処理を保証するために、ジョブ実行の適切な時間は午前零時です。  

### <a name="calculate-rollup-field"></a>ロールアップ フィールドの計算 

**ロールアップ フィールドの計算**は、指定したエンティティの既存のレコードのすべてのロールアップ フィールドの逐次計算を実行する定期的なジョブです。 エンティティごとに、**ロールアップ フィールド**ジョブが １ つだけあります。 逐次計算とは、最後の**ロールアップ フィールドの一括計算**ジョブの実行の終了後に、作成、更新、または削除されたレコードを、**ロールアップ フィールドの計算**ジョブが処理することを意味します。 既定の最大反復設定は 1 時間です。 エンティティの最初のロールアップ フィールドが作成されるときにジョブが自動的に作成され、最後のロールアップ フィールドが削除されるときにジョブが削除されます。  

## <a name="online-recalculation-option"></a>オンライン再計算オプション
下記に示されるように、フォームのロールアップ フィールドにマウス ポインタを重ねると、最後のロールアップの時間を表示できます。また、そのフィールドの横にある [更新] アイコンを選択して、ロールアップ値を更新できます。  

![取引先企業フォームのロールアップ フィールド](media/rollup-field-on-account-form.png)
  

オンライン再計算オプション (フォーム上の手動更新) を使用するとき、留意すべきいくつかの考慮事項があります。  
  
- エンティティに対する書き込み特権と、更新の対象となるソース レコードに対する書き込みアクセス権が必要です。 たとえば、取引先企業のオープンしている営業案件から売上見込みを計算するとき、書き込み特権は営業案件エンティティに対しては必要はありませんが、取引先企業エンティティに対してのみ必要です。  
- このオプションは、オンライン モードでのみ使用できます。 オフライン作業中は、ロールアップ フィールドは使用できません。  
- ロールアップ更新時の最大レコード数は 50,000 レコードに制限されます。 階層ロールアップ時には、その階層全体の関連レコードに適用されます。 制限を超えるとエラー メッセージが表示されます。*50,000 件の関連レコードの計算の限界に達したため、オンラインで計算を実行することができません。* ロールアップがシステム ジョブによって自動的に再計算されるときは、この限界は適用されません。  
- ソースレコードの最大の階層の深さの限界は 10 です。 制限を超えるとエラー メッセージが表示されます。*ソース レコードの階層の深さの限界の 10 に到達したので、オンラインで計算を実行することができません。* ロールアップがシステム ジョブによって自動的に再計算されるときは、この限界は適用されません。  

## <a name="modify-rollup-job-recurrence"></a>ロールアップ ジョブの定期的なアイテムの修正

システム管理者として、ロールアップ ジョブの反復のパターンを変更できます。また、ロールアップ ジョブを延期、一時停止、再開することができます。 ただし、ロールアップ ジョブを取り消し、または削除することはできません。 

定期的なアイテムのパターンを一時停止、延期、再開、または変更するには、システム ジョブを表示する必要があります。 詳細 [ロールアップ ジョブの表示](#view-rollup-jobs) 

ナビゲーション バーで、**アクション**を選択し、目的のアクションを選択します。 

**ロールアップ フィールドの一括計算**ジョブに使用できる選択肢: **再開**、**延期**、および**一時停止**。 

**ロールアップ フィールドの計算**ジョブの場合に使用できる選択肢: **定期的なアイテムの変更**、**再開**、**延期**、および**一時停止**。  
  
<a name="BKMK_businessscenarios"></a>  
 
## <a name="examples"></a>例 

いくつかのロールアップ フィールドの例を見てみましょう。 レコードのデータを、階層を使用して、また階層を使用せずに、関連レコードから集計します。 関連する活動から、また ActivityParty エンティティ経由でレコードに間接的に関連する活動からレコードのデータを集計することもできます。 各サンプルでは、フィールド エディターを使用して、ロールアップ フィールドを定義します。 フィールド エディターを開くには、ソリューション エクスプローラーを開き、**コンポーネント** > **エンティティ**を展開します。 必要なエンティティを選択し、**フィールド**を選択します。 **新規**を選択します。 エディターで、**フィールドの種類**および**データの種類**を含む必要な情報をフィールドに設定します。 データの種類の選択が終わったら、**フィールドの種類**で**ロールアップ**を選択します。 データ型には、小数、整数、通貨、および日時があります。 **フィールドの種類**の隣の**編集**ボタンを選択します。 これによって、ロールアップ フィールド定義エディターが表示されます。 ロールアップ フィールド定義は、**ソース エンティティ**、**関連エンティティ**、**集計**の 3 つのセクションから構成されます。  
  
-   **ソース エンティティ**セクションで、ロールアップ フィールドが定義されるエンティティを指定し、1 つの階層全体の集計を行うかどうかを指定します。 ロールアップの対象として使用する階層内のレコードを指定する、複数の条件を設定したフィルタを追加できます。  
  
-   **関連エンティティ**で、集計の対象とするエンティティを指定します。 ソース エンティティの階層でのロールアップを選択したとき、このセクションはオプションです。 計算で使用する関連レコードを指定する、複数の条件を設定したフィルタを追加できます。 たとえば、年間売り上げが $1000 を超える、オープンしている営業案件の売り上げを含めます。  
  
-   **集計**セクションで、計算の対象となるマトリックスを指定します。 SUM、COUNT、MIN、MAX または AVG などの使用できる集計関数を選択できます。  
  
### <a name="aggregate-data-for-a-record-from-related-records"></a>関連レコードからレコードのデータを集計する  

この例では、階層は使用されません。 取引先企業の合計売上見込みが、関連付けられたオープンしている営業案件から計算されます。  

![取引先企業の売上見込みの集計](media/rollup-field-no-hierarchy.png)
  
### <a name="aggregate-data-for-a-record-from-the-child-records-over-the-hierarchy"></a>レコードのデータを階層の全域の子レコードから集計する 
 
この例では、階層全域の、子営業案件を含む営業案件の合計売上見込みを計算します。  
  
![売上見込み、販売機会階層の集計](media/rollup-field-hierarchy-self.png)
  
### <a name="aggregate-data-for-a-record-from-the-related-records-over-the-hierarchy"></a>レコードのデータを階層の全域の関連レコードから集計する

この例では、階層全域の全取引先企業のオープンしている営業案件の合計売上見込みを計算します。  
  
![取引先企業階層の売上見込みの集計](media/rollup-field-hierarchy.png)  
  
### <a name="aggregate-data-for-a-record-from-all-related-activities"></a>すべての関連する活動からレコードのデータを集計する
  
この例では、費やされて請求の対象となる合計の時間を、取引先企業と関連するすべての活動から計算します。 これには、電話、予定、またはユーザー定義の活動で費やされた時間を含めることができます。  
  
以前のリリースでは、電話、FAX、予定などの個別の活動について、ロールアップ フィールドを定義できました。 しかし、次に示す例の結果を得るには、計算フィールドを使用してデータの集計をする必要がありました。 現在は、活動エンティティに対して 1 つのロールアップ フィールドを定義することによって、ワンステップでそれを行うことができます。  
  
![取引先企業のすべての活動のロールアップ](media/rollup-enhancements-activities.png)  
  
### <a name="aggregate-data-for-a-record-from-all-related-activities-and-activities-indirectly-related-via-the-activity-party-entity"></a>すべての関連する活動から、また活動関係者エンティティ経由でレコードに間接的に関連する活動からレコードのデータを集計する  

この例では、取引先企業に送信された電子メールの総数を計算します。この場合、取引先企業は電子メールの "宛先" 行または "CC 宛先" 行に記載されています。 これは、ロールアップ フィールド定義の定義活動関係者エンティティに対して、**フィルター**で**参加の種類**を指定して行います。 フィルターを使用しない場合、活動に対する使用可能なすべての参加の種類が計算に使用されます。 
 
特定の活動に対して使用可能な活動関係者エンティティと参加の種類の詳細については、「[ActivityParty エンティティ](/dynamics365/customer-engagement/developer/activityparty-entity)」を参照してください。

  
![関連する活動と活動関係者をロールアップ](media/rollup-enhancements-indirect-activities.png)  
  
### <a name="aggregate-data-for-a-record-from-related-records-using-the-avg-operator"></a>AVG 演算子を使用して、関連レコードからレコードのデータを集計する

この例では、取引先企業と関連するすべての営業案件から平均売上見込みを計算します。  
  
![Dynamics 365 の平均売上見込み](media/rollup-enhancements-average.PNG)  
  
次の例は、取引先企業の階層にわたる関連する営業案件から、平均の売り上げ見込みを計算する方法を示しています。 平均の売り上げ見込みを階層の各レベルで表示できます。  
  
![Dynamics 365 の平均売上見込み](media/cust-rollup-enhancements-avg-over-hierarchy.png)  
  
<a name="BKMK_considerations"></a> 

## <a name="rollup-field-considerations"></a>ロールアップ フィールドの考慮事項 

ロールアップ フィールドを使用するときは、次の特定の条件と制約に注意ください。  
  
- 組織については最大 100 のロールアップ フィールドを、各エンティティについては最大 10 のロールアップ フィールドを定義できます。  
- ワークフローをロールアップ フィールドの更新によって起動することはできません。  
- ワークフローの待機条件にロールアップ フィールドを使用することはできません。  
- ロールアップ フィールドに対するロールアップはサポートされません。  
- ロールアップは、他の計算フィールドのすべてのフィールドが現在のエンティティにある場合も、他の計算フィールドを使用する計算フィールドを参照できません。  
- ロールアップはフィルタを、ソース エンティティまたは関連エンティティ、単純なフィールドまたは複雑でない計算フィールドに追加できません。  
- ロールアップは、1:N の関連付けを持つ関連エンティティに対してのみ実行できます。 ロールアップは、N:N の関連付けに対しては実行できません。  
- ロールアップは、活動エンティティや活動関係者エンティティの 1:N の関連付けに対しては実行できません。  
- 業務ルール、ワークフロー、または計算フィールドは、ロールアップ フィールドの最終の計算された値を使用します。  
- ロールアップ フィールドは、システム ユーザーのコンテキストで集計されます。 すべてのユーザーに同じロールアップ フィールドの値を表示できます。 ロールアップ フィールドの表示を、フィールド レベル セキュリティ (FLS) を使用してロールアップ フィールドにアクセスできる者を制限することによって制御できます。 詳細[アクセスを制御するフィールド レベル セキュリティ](/dynamics365/customer-engagement/admin/field-level-security)。 

### <a name="precision-rounding"></a>丸め処理の精度
 
集計フィールドの小数点以下の桁数がロールアップ フィールドの小数点以下の桁数より多い場合、集計を実行する前に集計フィールドの桁数はロールアップの桁数に丸められます。 この動作を説明するために、特定の例を見てみましょう。 関連する営業案件の売上を予測している取引先企業エンティティのロールアップ フィールドには、小数点以下に 2 桁あると仮定しています。 推定 営業案件エンティティの売上見込みフィールドは、小数点以下の 4 桁の集計フィールドです。 この例では、取引先企業に 2 つの関連する営業案件が存在しています。 売上見込みの集計は次のとおりに計算されます:  
  
1. 推定 最初の営業案件の売上見込み: $1000.0041  
1. 推定 2番目の営業案件の売上見込み: $2000.0044  
1. 売り上げ見込みの集計 売上: $1000.00 + $2000.00 = $3000.00

このように、集計が実施される前に集計フィールドに小数点以下は 2 桁に丸められます。  
  
### <a name="different-behavior-from-associated-grids"></a>関連グリッドから別の動作
 
取引先企業や取引先担当者など一部のエンティティ フォームには、標準で、関連するグリッドが含まれています。 たとえば、取引先企業フォームには取引先担当者、サポート案件、営業案件や他のグリッドが含まれます。 取引先企業フォーム グリッドに表示されているレコードの一部は、直接的に取引先企業レコードに関連付けられます。他は、他のレコードと関連付けによって、間接に関連付けられます。 対照的に、ロールアップ フィールド集計は、ロールアップ フィールド定義で明示的に定義されている直接的な関連付けのみが使用されます。 他の関係は考慮されません。 動作の違いを説明するために、次の例を見てみましょう。  
  
1. 取引先企業 A1 には取引先責任者 P1 がいます。 サポート案件 C1 は取引先企業 A1 に関連付けられ (C1 顧客フィールド = A1)、サポート案件 C2 は取引先担当者の P1 に関連付けられています (C2 顧客フィールド = P1)。  
1. A1 レコードの**取引先企業**フォームの**サポート案件**は、2 つのサポート案件、C1 と C2 を表示します。  
1. サポート案件の合計数という取引先企業エンティティのロールアップ フィールドは、取引先企業に関連付けられたサポート案件に使用されます。  
1. 取引先企業ロールアップ フィールド定義で、取引先企業と顧客間関係があるサポート案件を指定します。 集計後、サポート案件の合計数は 1 になります。(サポート案件 C1) サポート案件 C2 は、取引先企業ではなく取引先担当者と直接関連付けられており、取引先企業ロールアップ フィールド定義で明示的に定義できないため、合計に含まれません。 そのため、ロールアップの操作から戻されるサポート案件の合計数は、**サポート案件**グリッドで示されるサポート案件の件数と一致しません。  
  
### <a name="see-also"></a>関連項目  

[フィールドの作成および編集](create-edit-fields.md)<br />
[計算フィールドの定義](define-calculated-fields.md)<br />
[日時フィールドの動作と形式](behavior-format-date-time-field.md)<br />
[階層的に関連するデータの定義とクエリ](define-query-hierarchical-data.md)<br />
[ビデオ: ロールアップ フィールドと計算フィールド](http://www.youtube.com/watch?v=RoahCH1p3T8&list=PLC3591A8FE4ADBE07&index=8)<br />
[ビデオ: Power BI の使用](http://www.youtube.com/watch?v=PkQe4BFlBS8&list=PLC3591A8FE4ADBE07&index=3)