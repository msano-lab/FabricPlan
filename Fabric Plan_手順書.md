# Fabric Plan ハンズオン手順書

# Step1：事前準備

## 概要

本ステップでは、Fabric Planの作成に必要な事前準備を行います。

Power BI DesktopからレポートをFabricワークスペースへ発行し、発行によって作成されたセマンティックモデルをPlanの参照元として用意します。

また、Writebackで使用するためのSQL Databaseを作成します。

## 手順

1. **レポートの発行**

    1. **Power BI Desktopからレポートを発行する**

        Power BI Desktopで **Plan.pbix** を開き、画面上部の **発行** を選択します。

        発行先として **Plan_workshop** ワークスペースを選択し、発行を完了します。

        ![レポート発行](../Step1_事前準備/images/1.1.png)

2. **Microsoft Fabricのワークスペース「Plan_workshop」にアクセスする**

    1. Fabricの「**Plan_workshop**」ワークスペースへアクセスし、レポートとセマンティックモデルが発行されていることを確認します。

        ![ワークスペースへアクセス](../Step1_事前準備/images/2.1.png)

        ![レポート・セマンティックモデルの確認](../Step1_事前準備/images/2.1.2.png)

3. **SQL DBの作成**

    1. 「**＋新しい項目**」をクリックし、「**SQL database**」を選択します。
        ![SQL DBの作成](../Step1_事前準備/images/3.1.png)

    2. 「**DB_ご自身の苗字（半角英字）**」を入力し、「**作成**」をクリックします。　※本手順書では「**name**」と入力します。
        ![SQL DBの作成](../Step1_事前準備/images/3.2.png)

    3. SQL DBが作成されます。
        ![SQL DBの作成](../Step1_事前準備/images/3.3.png)

4. **Planの作成**

    1. ワークスペース「**Plan_workshop_ご自身の苗字（半角英字）**」に戻り、**＋新しい項目** > **プラン** > **Plan_ご自身の苗字（半角英字）** > **作成** の順に選択し、Planを作成します。
        ![Planの作成](../Step1_事前準備/images/4.1.png)

        ![Planの作成](../Step1_事前準備/images/4.1.2.png)

        ![Planの作成](../Step1_事前準備/images/4.1.3.png)

        ![Planの作成](../Step1_事前準備/images/4.1.4.png)

5. **データの取得**

    1. **Get Data**の「**Semantic Model**」をクリックします。
        ![データの取得](../Step1_事前準備/images/5.1.png)

    2. 「**＋Create Connection**」をクリックします。
        ![データの取得](../Step1_事前準備/images/5.2.png)

    3. 以下の情報を設定し、**Create** をクリックします。

        | 設定項目 | 設定値 |
        |---|---|
        | 接続 | **新しい接続の作成** |
        | 接続名 | **Plan_workshop_ご自身の苗字（半角英字）** |
        | 認証の種類 | **組織アカウント** |
        | サインイン | **ボタンをクリックし、サインイン** |

        ![データの取得](../Step1_事前準備/images/5.3.png)

    4. 「**Select Semantic Model**」をクリックします。
        ![データの取得](../Step1_事前準備/images/5.4.png)

    5. **Plan** を選択し、**追加** をクリックします。

        ![データの取得](../Step1_事前準備/images/5.5.png)

    6. **Connect** をクリックします。

        ![データの取得](../Step1_事前準備/images/5.6.png)

    7. Dataにセマンティックモデルが追加されます。
        ![データの取得](../Step1_事前準備/images/5.7.png)

## Step1 まとめ

以上で、**Step0「事前準備」** は完了です。

本ステップでは、以下の作業を実施しました。

- Fabricワークスペースへのセマンティックモデルの発行
- Writebackで使用するSQL Databaseの作成
- Planの作成およびセマンティックモデルとの接続

これにより、以降のStepでFabric Planの各機能を操作するための準備が整いました。

---

# Step2：入力列の作成

## 概要

本ステップでは、予算管理用のPlanning Sheetに予算入力と承認に必要な項目を追加し、データ入力のための構成を整えます。


## 手順

1. **予算管理シートの作成**

    1. **New Planning Sheet** > **Name** に「**YOSAN_KANRI**」を入力し、**Create** をクリックします。
        ![Planning Sheetの作成](../Step2_入力列の作成/images/1.1.png)

2. **マトリックスの作成**

    1. データペインからフィールドペインへドラッグアンドドロップし、以下の項目を設定します。

        | 設定項目 | 設定値 |
        |---|---|
        | **Rows** | **05_M_SHOUHIN**（**CATEGORY**、**BRAND**、**VARIATION**） |
        | **Columns** | **CALENDAR**（**DATE_Hierarchy**） |
        | **Values** | **MEASURE**（**URIAGE**、**ZENNEN_URIAGE**） |

        ![マトリックスの作成](../Step2_入力列の作成/images/2.1.png)

3. **合計、小計の管理**

    1. **Planning**タブ > **Σ** > 以下のとおり設定します。

        | 設定項目 | 設定値 |
        |---|---|
        | **Column Grand Total** | **Left** |
        | **Column Subtotal** | **Right** |

        ![合計・小計の管理](../Step2_入力列の作成/images/3.1.png)

    2. Column Grand TotalとColumn Subtotalが追加されます。
        ![合計・小計の管理](../Step2_入力列の作成/images/3.2.png)

        ![合計・小計の管理](../Step2_入力列の作成/images/3.2.2.png)

4. **予算*1.07列の作成（Visual Measure）**

    1. **Planning**タブ > **Insert Column** > **Formula** を選択し、以下の情報を設定して **Create** をクリックします。

        | 設定項目 | 設定値 |
        |---|---|
        | **Title** | **YOSAN*1.07** |
        | **Insert as** | **Visual Measure** |
        | **Data type** | **Number** |
        | **Formula** | **[ZENNEN_URIAGE]*1.07** |
        | **Column aggregation type** | **Sum** |
        | **Row aggregation type** | **Formula** |

        ![予算*1.07列の作成](../Step2_入力列の作成/images/4.1.png)

        ![予算*1.07列の作成](../Step2_入力列の作成/images/4.1.2.png)

    2. 「YOSAN*1.07」列が作成されます。

        ※2024年以降のデータを取り込んでいるため、2024年は前年売上がありません。したがって「YOSAN*1.07」列も空白となります。

        ![予算*1.07列の作成](../Step2_入力列の作成/images/4.2.png)

5. **前年ベース予算列の作成**

    1. **Planning**タブ > **Insert Column** > **Number** > **Copy from another series** > **ZENNEN_URIAGE** を選択し、以下の情報を設定して **Create** をクリックします。

        | 設定項目 | 設定値 |
        |---|---|
        | **Title** | **YOSAN_PYBASE** |
        | **Insert as** | **Visual Measure** |
        | **Column aggregation type** | **Sum** |
        | **Row aggregation type** | **Sum** |

        ![前年ベース予算列の作成](../Step2_入力列の作成/images/5.1.png)

        ![前年ベース予算列の作成](../Step2_入力列の作成/images/5.1.2.png)

    2. 「YOSAN_PYBASE」列が作成されます。

        ※2024年以降のデータを取り込んでいるため、2024年は前年売上がありません。したがって「YOSAN_PYBASE」列も空白となります。

        ![前年ベース予算列の作成](../Step2_入力列の作成/images/5.2.png)


6. **予算入力列の作成**

    1. **Planning**タブ > **Insert Column** > **Number** > **Insert a new series** を選択し、以下の情報を設定して **Create** をクリックします。

        | 設定項目 | 設定値 |
        |---|---|
        | **Title** | **YOSAN_INPUT** |
        | **Insert as** | **Visual Measure** |
        | **Input type** | **Number** |
        | **Column aggregation type** | **Sum** |
        | **Row aggregation type** | **Sum** |

        ![予算入力列の作成](../Step2_入力列の作成/images/6.1.png)

        ![予算入力列の作成](../Step2_入力列の作成/images/6.1.2.png)

    2. 「YOSAN_INPUT」列が作成されます。

        ![前年ベース予算列の作成](../Step2_入力列の作成/images/6.2.png)

    3. **2025年**の**YOSAN_INPUT列All行**をダブルクリック＞数式バーに「**700m**」を入力＞キーボードのEnterキーを押下すると、予算値が入力されます。
        
        ※デフォルトでは値は均等に配賦されます。

        ![前年ベース予算列の作成](../Step2_入力列の作成/images/6.3.png)

        ![前年ベース予算列の作成](../Step2_入力列の作成/images/6.3.2.png)

7. **前年売上の重みによる配賦**

    1. **2025年**の**YOSAN_INPUT列All行**を選択後、**配賦メニュー**をクリックして、**Distribute by weights of ZENNEN_URIAGE**＞2025年を選択します。

        ![前年売上の重みによる配賦](../Step2_入力列の作成/images/7.1.png)

    2. 6.3で入力した2025年の予算値が、2024年の売上構成比をもとに配賦されます。

        ![前年売上の重みによる配賦](../Step2_入力列の作成/images/7.2.png)

8. **トレンドによる配賦（列）**

    1. **2025年**の**YOSAN_INPUT列All行**を選択後、**配賦アイコン**をクリックし、**Distribute to columns with trend** > 「**6%**」に設定します。

        ![トレンドによる配賦](../Step2_入力列の作成/images/8.1.png)

    2. 指定したトレンド率は、配賦対象の最下層の期間単位に適用されます。
        ※今回の設定では、最下層の**月単位**で6%ずつ増加するトレンドとなるように配賦されています。

        ![トレンドによる配賦](../Step2_入力列の作成/images/8.2.png)

9. **コメント列の作成**

    1. **Planning**タブ > **Insert Column** > **Text** を選択し、以下の情報を設定して **Create** をクリックします。

        | 設定項目 | 設定値 |
        |---|---|
        | **Title** | **Comment** |
        | **Insert as** | **Visual Column** |
        | **Input type** | **Short Text** |

        ![コメント列の作成](../Step2_入力列の作成/images/9.1.png)

        ![コメント列の作成](../Step2_入力列の作成/images/9.1.2.png)

    2. マトリックスの右端に「Comment」列が作成されます。
        ※「**Insert as**」で「**Visual Column**」を選択すると、既存のマトリックスの右端に独立した列として追加されます。

        　「**Visual Measure**」選択すると、独立した列ではなく、マトリックス内のメジャーとして追加されます。

        ![コメント列の作成](../Step2_入力列の作成/images/9.2.png)

    3. **Comment**列の任意のセルをダブルクリックし、テキストを入力します。
        ![コメント列の作成](../Step2_入力列の作成/images/9.3.png)

10. **承認ステータス列の作成**

    1. **Planning**タブ > **Insert Column** > **List** > **Single Select** を選択し、以下の情報を設定して **Create** をクリックします。

        | 設定項目 | 設定値 |
        |---|---|
        | **Title** | **SHONIN_STATUS** |
        | **Insert as** | **Visual Column** |
        | **Input type** | **Single Select** |
        | **Options** | **Presets** > **Approval Status** > **Apply** |
        | **Default Value** | **Static** |
        | **Value** | **Submitted** |

        ![承認ステータス列の作成](../Step2_入力列の作成/images/10.1.png)

        ![承認ステータス列の作成](../Step2_入力列の作成/images/10.1.2.png)

        ![承認ステータス列の作成](../Step2_入力列の作成/images/10.1.3.png)

    2. 「SHONIN_STATUS」列が作成されます。

        ![承認ステータス列の作成](../Step2_入力列の作成/images/10.2.png)    

    3. **SHONIN_STATUS**列の「雷神エナジー」のセルをクリックし、**In Review**を選択します。

        ![承認ステータス列の作成](../Step2_入力列の作成/images/10.3.png)

    4. ステータスが「**In Review**」に変更されます。

        ![承認ステータス列の作成](../Step2_入力列の作成/images/10.4.png)

    5. **コピーアイコン** > **Copy to all rows in 雷神エナジー**を選択します。

        ![承認ステータス列の作成](../Step2_入力列の作成/images/10.5.png)

        ![承認ステータス列の作成](../Step2_入力列の作成/images/10.5.2.png)

11. **最終承認列の作成**

    1. **Planning**タブ > **Insert Column** > **Checkbox** を選択し、以下の情報を設定して **Create** をクリックします。

        | 設定項目 | 設定値 |
        |---|---|
        | **Title** | **SAISHU_SHONIN** |
        | **Insert as** | **Visual Column** |
        | **Input type** | **Checkbox** |
        | **Default Value** | **Static** |
        | **Value** | **Unchecked** |

        ![最終承認列の作成](../Step2_入力列の作成/images/11.1.png)

        ![最終承認列の作成](../Step2_入力列の作成/images/11.1.2.png)

    2. 「SAISHU_SHONIN」列が作成されます。

        ![最終承認列の作成](../Step2_入力列の作成/images/11.2.png)

12. **承認者列の作成**

    1. **Planning**タブ > **Insert Column** > **Person** を選択し、以下の情報を設定して **Create** をクリックします。

        | 設定項目 | 設定値 |
        |---|---|
        | **Title** | **SHONINSHA** |
        | **Insert as** | **Visual Column** |
        | **Input type** | **Person** |

        ![承認者列の作成](../Step2_入力列の作成/images/12.1.png)

        ![承認者列の作成](../Step2_入力列の作成/images/12.1.2.png)

    2. 「SHONINSHA」列が作成されます。

        ![承認者列の作成](../Step2_入力列の作成/images/12.2.png)

    3. 任意のセルをクリックすると、組織のMicrosoft Entra IDに登録されているユーザーを選択できます。

        ※「Person列では、ワークスペースのメンバーに限らず、組織のMicrosoft Entra IDに登録されているユーザーを選択できます。
        
            なお、選択したユーザーがPlanを閲覧・編集するには、対象ワークスペースまたはPlanアイテムへのアクセス権が別途必要です。

        ![最終承認列の作成](../Step2_入力列の作成/images/12.3.png)

13. **承認期限列の作成**

    1. **Planning**タブ > **Insert Column** > **Date** を選択し、以下の情報を設定して **Create** をクリックします。

        | 設定項目 | 設定値 |
        |---|---|
        | **Title** | **SHONIN＿KIGEN** |
        | **Insert as** | **Visual Column** |
        | **Input type** | **Date** |
        | **Format** | **Default Locale** |
        | **Minimum Date** | **今日の日付** |
        | **Maximum Date** | **今月末の日付** |
        | **Default Value** | **Static** |
        | **Value** | **今日の日付** |

        ![承認期限列の作成](../Step2_入力列の作成/images/13.1.png)

        ![承認期限列の作成](../Step2_入力列の作成/images/13.1.2.png)

    2. 「SHONIN_KIGEN」列が作成されます。

        ![承認期限列の作成](../Step2_入力列の作成/images/13.2.png)

14. **ルール（最小値・最大値）の設定**

    1. **Model**タブ > **Rules** > **Minmax rule** を選択し、以下の情報を設定して **Create** をクリックします。

        | 設定項目 | 設定値 |
        |---|---|
        | **Minimum Value** | **Static**、**10000000** |
        | **Maximum Value** | **Static**、**20000000** |
        | **Rows Selection** | **Custom** > **雷神エナジー** |
        | **Columns Selection** | **Custom** > **2026年Q3** |

        ![ルール（最小値・最大値）の設定](../Step2_入力列の作成/images/14.1.png)

        ![ルール（最小値・最大値）の設定](../Step2_入力列の作成/images/14.1.2.png)

    2. **2026年Q3の雷神エナジー**のセルで「**5m**」を入力し、ルールが適用されたことを確認します。
        ![ルール（最小値・最大値）の設定](../Step2_入力列の作成/images/14.2.png)

        ![ルール（最小値・最大値）の設定](../Step2_入力列の作成/images/14.2.2.png)

15. **セルのロック**

    1. 任意のセルを選択し、**配賦メニュー** > **Lock all children** を選択します。
        ![セルのロック](../Step2_入力列の作成/images/15.1.png)

    2. セルをクリックし、ロックされていることを確認します。
        ![セルのロック](../Step2_入力列の作成/images/15.2.png)

16. **キューブの作成**

    1. **Planning**タブ > **Insert Column** > **Number** > **Insert a new empty series** > **＋Add Breakdown** を選択し、以下の情報を設定して **Create** をクリックします。

        | 設定項目 | 設定値 |
        |---|---|
        | **Title** | **YOSAN_CUBE** |
        | **Reference Measures** | **ZENNEN_URIAGE** |
        | **Breakdown1** | **05_M_SHOHIN[CATEGORY]**、**[BRAND]**、**[VARIATION]** |
        | **Breakdown2** | **05_M_SHOHIN[CATEGORY]**、**02_M_CHIIKI[CHIIKI_NAME]**、**01_M_TODOFUKEN[TODOFUKEN_NAME]** |

        ![キューブの作成](../Step2_入力列の作成/images/16.1.png)

        ![キューブの作成](../Step2_入力列の作成/images/16.1.2.png)

        ![キューブの作成](../Step2_入力列の作成/images/16.1.3.png)

        ![キューブの作成](../Step2_入力列の作成/images/16.1.4.png)

    2. 「YOSAN_CUBE」列が作成されます。

        ![キューブの作成](../Step2_入力列の作成/images/16.2.png)

17. **地域別予算管理シートの作成**

    1. **Home**タブ > **New Planning Sheet** > 名前に「**YOSAN_KANRI_CHIIKI**」を入力し、地域別予算管理シートを作成します。
        ![地域別予算管理シートの作成](../Step2_入力列の作成/images/17.1.png)

18. **マトリックスの作成**

    1. データペインからフィールドペインへドラッグアンドドロップし、以下の項目を設定します。

        | 設定項目 | 設定値 |
        |---|---|
        | **Rows** | **02_M_CHIIKI[CHIIKI_NAME]**、**01_M_TODOFUKEN[TODOFUKEN_NAME]** |
        | **Columns** | **CALENDAR**[DATE_Hierarchy] |
        | **Values** | **MEASURE[ZENNEN_URIAGE]** |

        ![マトリックスの作成](../Step2_入力列の作成/images/18.1.png)

19. **マトリックスへキューブを追加**

    1. データペイン > **From Sheets** > **Cube** > **YOSAN_CUBE** > 「**…**」 > **Insert as a measure** をクリックします。

        ![マトリックスへキューブを追加](../Step2_入力列の作成/images/19.1.png)

    2. **2025年**を展開し、**Q4**の**All**セルに「**200m**」を入力します。

        ![マトリックスへキューブを追加](../Step2_入力列の作成/images/19.2.png)

        ![マトリックスへキューブを追加](../Step2_入力列の作成/images/19.2.2.png)

    3. **YOSAN_KANRI**シートに戻り、値が反映されていることを確認します。

        ![マトリックスへキューブを追加](../Step2_入力列の作成/images/19.3.png)

    4. **Q3**の**Allセル**に**190m**を入力します。

        ![マトリックスへキューブを追加](../Step2_入力列の作成/images/19.4.png)

        ![マトリックスへキューブを追加](../Step2_入力列の作成/images/19.4.2.png)

    5. **YOSAN_KANRI_CHIIKI**シートへ戻り、値が反映されていることを確認します。

        ![マトリックスへキューブを追加](../Step2_入力列の作成/images/19.5.png)

## Step2 まとめ

以上で、**Step1「入力列の作成」** は完了です。

本ステップでは、以下の作業を実施しました。

- 予算管理シートの作成
- 計算、入力、コメント、承認に関する項目の設定
- 値の配賦、入力ルール、セルのロックの設定
- キューブと地域別予算管理シートの作成および多次元配賦

これにより、予算の入力や配賦、承認、地域別の管理に必要な設定が整いました。

---

# Step3：予測

## 概要

本ステップでは、予測用のPlanning Sheetを作成し、予測期間（Closed Period、Open Period）の設定と値の入力を行います。

また、再予測や統計予測を実施し、実績や過去データをもとに将来の予測値を更新・作成します。


## 手順

1. **予測シートの作成**

    1. **Home**タブ > **New Planning Sheet** > 名前に「**YOSOKU**」を入力し、予測シートを作成します。
        ![予測シートの作成](../Step3_予測/images/1.1.png)

2. **マトリックスの作成**

    1. データペインからフィールドペインへドラッグアンドドロップし、以下の項目を設定します。

        | 設定項目 | 設定値 |
        |---|---|
        | **Rows** | **05_M_SHOHIN**（**[CATEGORY]**、**[BRAND]**、**[VARIATION]**） |
        | **Columns** | **CALENDAR[DATE_Hierarchy]** |
        | **Values** | **MEASURE**（**[URIAGE]**、**[ZENNEN_URIAGE]**） |

        ![マトリックスの作成](../Step3_予測/images/1.2.png)

3. **予測列の作成（Open Period：Data Input）**

    1. **Model**タブ > **Forecast** を選択し、以下の情報を設定して **Next** をクリックします。

        | 設定項目 | 設定値 |
        |---|---|
        | **Measure Name** | **YOSOKU** |
        | **Forecast Period** | **Jun 2026 - Sep 2026** |

        ![予測列の作成](../Step3_予測/images/3.1.png)

    2. Closed Period（閉鎖期間）について以下の情報を設定して **Next** をクリックします。

        | 設定項目 | 設定値 |
        |---|---|
        | **Configure as** | **Link to Measure**|
        | **Source Measure** | **URIAGE** |

        ![予測列の作成](../Step3_予測/images/3.2.png)

    3. Open Period（開放期間）について以下の情報を設定して **Save** をクリックします。

        | 設定項目 | 設定値 |
        |---|---|
        | **Configure as** | **Data Input** |
        | **Default Value** | **None** |

        ※**Pre fill Open Periods**を使用すると、期間ごとに予測方法を設定できます。

        ![予測列の作成](../Step3_予測/images/3.3.png)

    4. 「YOSOKU」列が作成されます。
        ※Closed Period（閉鎖期間）はグレーで表示され、編集不可に設定されています。

        ![予測列の作成](../Step3_予測/images/3.4.png)

4. **予測値の入力**

    1. **2026年6月〜9月セル**で予測値を入力します。

        ![予測値の入力](../Step3_予測/images/4.1.png)

5. **再予測**

    1. **Model**タブ > **Reforecast** > **Reforecast Column** > 下記情報を設定して、**Apply** をクリックします。

        | 設定項目 | 設定値 |
        |---|---|
        | **Target Period** | **Jun2026 - Sep2026** |
        | **Copy Source** | **URIAGE** |
        | **Apply Operation** | **Period Range** |
        | **Source Periods** | **Jun2025 - Sep2025** |

        ![再予測](../Step3_予測/images/5.1.png)

        ![再予測](../Step3_予測/images/5.1.2.png)

    2. 2026年6月～9月の値に、2025年6月～9月の「URIAGE」列の値がコピーされたことを確認します。

        ![再予測](../Step3_予測/images/5.2.png)

6. **予測期間の編集**

    1. **Model**タブ > **Period** > **Close Period** > 以下の情報を設定して **Preview** ＞ **Save** をクリックします。

        | 設定項目 | 設定値 |
        |---|---|
        | **Select Measure** | **YOSOKU** |
        | **Close Period till** | **Custom** |
        | **Selected Period** | **Jun 2026** |
        | **Extend Forecast Range** | **チェックを入れる > 1 Month** |

        ![予測期間の変更](../Step3_予測/images/6.1.png)

        ![予測期間の変更](../Step3_予測/images/6.1.2.png)

        ![予測期間の変更](../Step3_予測/images/6.1.3.png)

    2. 2026年6月の「YOSOKU」列がクローズされ、新たに2026年10月に「YOSOKU」列が追加されたことを確認します。

        ![予測期間の変更](../Step3_予測/images/6.2.png)

    3. 補足：予測期間は以下の手順で変更することも可能です。
        **Planning**タブ > **Insert Column** > **Manage measures** > **Revenue Forecast** の鉛筆マークを選択し、
        **Forecast Period** を翌年12月に変更して、**Update** をクリックします。

        ![予測期間の変更](../Step3_予測/images/6.3.png)

        ![予測期間の変更](../Step3_予測/images/6.3.2.png)

        ![予測期間の変更](../Step3_予測/images/6.3.3.png)

7. **統計予測列の作成**

    1. **Model**タブ > **Forecast** > 以下の情報を設定して**Next** をクリックします。

        | 設定項目 | 設定値 |
        |---|---|
        | **Measure Name** | **TOUKEI_YOSOKU** |
        | **Forecast Period** | **Jul 2026 - Sep 2026** |

        ![統計予測列の作成](../Step3_予測/images/7.1.png)

    2. Closed Period（閉鎖期間）について以下の情報を設定して **Next** をクリックします。

        | 設定項目 | 設定値 |
        |---|---|
        | **Configure as** | **Link to Measure** |
        | **Source Measure** | **URIAGE** |

        ![統計予測列の作成](../Step3_予測/images/7.2.png)

    3. Open Period（開放期間）について以下の情報を設定して **Save** をクリックします。

        | 設定項目 | 設定値 |
        |---|---|
        | **Configure as** | **Data Input** |
        | **Default Value** | **None** |

        ![統計予測列の作成](../Step3_予測/images/7.3.png)

    4. 「TOUKEI_YOSOKU」列が作成されます。

        ![統計予測列の作成](../Step3_予測/images/7.4.png)

    5. **2026年7月** の「**TOUKEI_YOSOKU**」列 **スポーツ飲料** のセルを選択し、
       **Model**タブ > **Predict** をクリックします。

       ![統計予測列の作成](../Step3_予測/images/7.5.png)
       
    6. **Growth Factor** を **6%** に設定して、
       **Run Forecast** > **Save Forecast** > **Save** をクリックします。

       ![統計予測列の作成](../Step3_予測/images/7.6.png)

    7. 予測値を確認し、 **Save Forecast** ＞ **Save** をクリックします。

        ![統計予測列の作成](../Step3_予測/images/7.7.png)

        ![統計予測列の作成](../Step3_予測/images/7.7.2.png)

    8. 値が反映されたことを確認します。

        ![統計予測列の作成](../Step3_予測/images/7.8.png)

## Step3 まとめ

以上で、**Step2「予測」** は完了です。

本ステップでは、以下の作業を実施しました。

- 予測シートの作成
- 予測列と予測期間の設定
- 再予測
- 統計予測の作成

これにより、実績や過去データをもとに将来の予測値を作成し、継続的に計画を更新できるようになります。

---

# Step4：シミュレーション

## 概要

本ステップでは、シミュレーション用のPlanning Sheetを作成し、シミュレーション値の個別調整および一括編集を行います。

これにより、設定したシミュレーション値が結果に与える影響を試算できるようにします。

## 手順

1. **シミュレーションシートの作成**

    1. **Home**タブ > **New Planning Sheet** > 名前に「**SIMULATION**」を入力し、シミュレーションシートを作成します。

        ![シミュレーションシートの作成](../Step4_シミュレーション/images/1.1.png)

2. **マトリックスの作成**

    1. データペインからフィールドペインへドラッグアンドドロップし、以下の項目を設定します。

        | 設定項目 | 設定値 |
        |---|---|
        | **Rows** | **05_M_SHOHIN**（**[CATEGORY]**、**[BRAND]**、**[VARIATION]**） |
        | **Columns** | **CALENDAR**（**DATE_Hierarchy**） |
        | **Values** | **Measure Table**（**[ZENNEN_URIAGE]**） |

        ![マトリックスの作成](../Step4_シミュレーション/images/2.1.png)

3. **売上列の作成**

    1. **Planning**タブ > **Insert Column** > **Simulate** > 以下の情報を設定して **Create** をクリックします。

        | 設定項目 | 設定値 |
        |---|---|
        | **Title** | **URIAGE (Simulation)** |
        | **Insert as** | **Visual Measure** |
        | **Simulation based on** | **ZENNEN_URIAGE** |
        | **Variance formatting style** | **Positive** |
        | **Value Range** | **±100** |
        | **Simulation Value** | **Left** |
        | **Allow Input** | **In both read and edit mode** |

        ![売上列の作成](../Step4_シミュレーション/images/3.1.png)

        ![売上列の作成](../Step4_シミュレーション/images/3.1.2.png)

    2. 「URIAGE（Simulation）」列が作成されます。

        ![売上列の作成](../Step4_シミュレーション/images/3.2.png)

4. **シミュレーションスライダーの設定**

    1. **2026年Q1** の **雷神エナジー** のセルを選択し、スライダーを使用してシミュレーション値を調整します。
        ※**Ctrl**キーを押しながら複数のセルを選択して、同時に調整することも可能です。

        ![シミュレーションスライダーの設定](../Step4_シミュレーション/images/4.1.png)

5. **一括編集（Bulk Edit）**

    1. **Planning**タブ > **Bulk Edit** > 下記の情報を設定して **Apply** をクリックします。

        | 設定項目 | 設定値 |
        |---|---|
        | **Measure** | **URIAGE（Simulation）** |
        | **Filter** | **＋ Add Filter** > **BRAND is 匠珈琲** |
        | **Apply to Row Level** | **VARIATION** |
        | **Apply to Column Level** | **quarter** |
        | **Simulation** | **5** |

        ![Bulk Edit](../Step4_シミュレーション/images/5.1.png)

    2. シミュレーション値が一括で編集されていることを確認します。

        ![Bulk Edit](../Step4_シミュレーション/images/5.2.png)

## Step4 まとめ

以上で、**Step3「シミュレーション」** は完了です。

本ステップでは、以下の作業を実施しました。

- シミュレーションシートの作成
- URIAGE（Simulation）列の作成
- シミュレーションスライダーの設定
- Bulk editによる一括更新

これにより、実績値や想定値をもとに売上の変動をシミュレーションし、その結果を計画の検討・調整に活用できるようになります。

---

# Step5：最適化

## 概要

本ステップでは、利益計画用のPlanning Sheetを作成し、売上・仕入額・輸送費の計画列と利益計画列を設定します。

また、各計画値に条件を設定し、目標利益に基づく最適化と、利益最大化のための最適化を行います。

## 手順

1. **利益計画シートの作成**

    1. **Home**タブ > **New Planning Sheet** > 名前に「**RIEKI_KEIKAKU**」を入力し、利益計画シートを作成します。

        ![利益計画シートの作成](../Step5_最適化/images/1.1.png)

2. **マトリックスの作成**

    1. データペインからフィールドペインへドラッグアンドドロップし、以下の項目を設定します。

        | 設定項目 | 設定値 |
        |---|---|
        | **Rows** | **02_M_CHIIKI**（**[CHIIKI_NAME]**、**01_M_TODOFUKEN**（**[TODOFUKEN_NAME]**） |
        | **Columns** | **CALENDAR**（**DATE_Hierarchy**） |
        | **Values** | **Measures Table**（**[ZENNEN_RIEKI]**、**[ZENNEN_URIAGE]**、**[ZENNEN_SHIIREGAKU]**、**[ZENNEN_YUSOHI]**） |

        ![マトリックスの作成](../Step5_最適化/images/2.1.png)

3. **売上計画列の作成**

    1. **Planning**タブ > **Insert Column** > **Copy from another series** > **ZENNEN_URIAGE** > 下記情報を設定して **Create** をクリックします。

        | 設定項目 | 設定値 |
        |---|---|
        | **Title** | **URIAGE_PLAN** |
        | **Insert as** | **Visual Measure** |
        | **Input type** | **Number** |
        | **Column aggregation type** | **Sum** |
        | **Row aggregation type** | **Sum** |
        | **Distribute parent value to children** | **チェックを入れる** |

        ![売上計画列の作成](../Step5_最適化/images/3.1.png)

        ![売上計画列の作成](../Step5_最適化/images/3.1.2.png)

    2. 「URIAGE_PLAN」列が作成されます。

        ![売上計画列の作成](../Step5_最適化/images/3.2.png)

4. **仕入額計画列の作成**

    1. **Planning**タブ > **Insert Column** > **Copy from another series** > **ZENNEN_SHIIREGAKU** > 下記情報を設定して **Create** をクリックします。

        | 設定項目 | 設定値 |
        |---|---|
        | **Title** | **SHIIREGAKU_PLAN** |
        | **Insert as** | **Visual Measure** |
        | **Input type** | **Number** |
        | **Column aggregation type** | **Sum** |
        | **Row aggregation type** | **Sum** |
        | **Distribute parent value to children** | **チェックを入れる** |

        ![仕入額計画列の作成](../Step5_最適化/images/4.1.png)

        ![仕入額計画列の作成](../Step5_最適化/images/4.1.2.png)

    2. 「SHIIREGAKU_PLAN」列が作成されます。

        ![仕入額計画列の作成](../Step5_最適化/images/4.2.png)

5. **輸送費計画列の作成**

    1. **Planning**タブ > **Insert Column** > **Copy from another series** > **ZENNEN_YUSOHI** > 下記情報を設定して **Create** をクリックします。

        | 設定項目 | 設定値 |
        |---|---|
        | **Title** | **YUSOHI_PLAN** |
        | **Insert as** | **Visual Measure** |
        | **Input type** | **Number** |
        | **Column aggregation type** | **Sum** |
        | **Row aggregation type** | **Sum** |
        | **Distribute parent value to children** | **チェックを入れる** |

        ![輸送費計画列の作成](../Step5_最適化/images/5.1.png)

        ![輸送費計画列の作成](../Step5_最適化/images/5.1.2.png)

    2. 「YUSOHI_PLAN」列が作成されます。

        ![輸送費計画列の作成](../Step5_最適化/images/5.2.png)

6. **利益計画列の作成**

    1. **Planning**タブ > **Insert Column** > **Formula** > 下記情報を設定して **Create** をクリックします。

        | 設定項目 | 設定値 |
        |---|---|
        | **Title** | **RIEKI_PLAN** |
        | **Insert as** | **Visual Measure** |
        | **Data type** | **Number** |
        | **Formula** | **[URIAGE_PLAN] - [SHIIREGAKU_PLAN] - [YUSOHI_PLAN]** |
        | **Column aggregation type** | **Formula** |
        | **Row aggregation type** | **Formula** |

        ![利益計画列の作成](../Step5_最適化/images/6.1.png)

        ![利益計画列の作成](../Step5_最適化/images/6.1.2.png)

    2. 「RIEKI_PLAN」列が作成されます。

        ![輸送費計画列の作成](../Step5_最適化/images/6.2.png)

7. **表示項目の管理**

    1. **Planning**タブ > **Show Columns** > 下記の項目のチェックを外します。

        - **ZENNEN_URIAGE**
        - **ZENNEN_SHIIREGAKU**
        - **ZENNEN_YUSOHI**

        ![表示項目の管理](../Step5_最適化/images/7.1.png)

    2. チェックを外した項目が、マトリックス上で非表示になったことを確認します。

        ![表示項目の管理](../Step5_最適化/images/7.2.png)

8. **列の順序入れ替え**

    1. **RIEKI_PLAN列** をドラッグアンドドロップで **ZENNEN_RIEKI列** の右隣に移動します。

        ![列の順序入れ替え](../Step5_最適化/images/8.1.png)

9. **目標値に基づく計画の最適化**

    1. **2026年** の**RIEKI_PLAN列 ALLセル** を選択し、**Planning**タブ > **・・・** > **Optimize** をクリックします。

        ![計画の最適化](../Step5_最適化/images/9.1.png)

    2. 以下の情報を設定して **Next** をクリックします。
        ※ **Objective** を **Target** にすることで、**RIEKI_PLAN** が指定した目標値に近づくように最適化します。

        | 項目 | 設定値 |
        |---|---|
        | **Objective** | **Target** |
        | **Target Value** | **420m** |
        | **Variables to Update** | **[URIAGE_PLAN]**、**[SHIIREGAKU_PLAN]**、**[YUSOHI_PLAN]** |

        ![計画の最適化](../Step5_最適化/images/9.2.png)

    3. **＋ Add Constraint** をクリックし、以下の情報を設定して **Apply** をクリックします。

        | 項目 | 設定値 |
        |---|---|
        | **Apply to Variable** | **URIAGE_PLAN** |
        | **Set Type** | **Range** |
        | **Min** | **765m** |
        | **Max** | **775m** |

        ![計画の最適化](../Step5_最適化/images/9.3.png)

        ![計画の最適化](../Step5_最適化/images/9.3.2.png)

    4. **＋ Add** をクリックし、以下の情報を設定して **Apply** をクリックします。

        | 項目 | 設定値 |
        |---|---|
        | **Variable** | **SHIIREGAKU_PLAN** |
        | **Set Type** | **Range** |
        | **Min** | **325m** |
        | **Max** | **330m** |

        ![計画の最適化](../Step5_最適化/images/9.4.png)

    5. **＋ Add** をクリックし、以下の情報を設定して **Apply** をクリックします。

        | 項目 | 設定値 |
        |---|---|
        | **Variable** | **YUSOHI_PLAN** |
        | **Set Type** | **Range** |
        | **Min** | **21m** |
        | **Max** | **22m** |

        ![計画の最適化](../Step5_最適化/images/9.5.png)

    6. **Run** をクリックし、2026年の利益計画を最大化する最適解を確認後、**Apply** をクリックします。

        ![計画の最適化](../Step5_最適化/images/9.6.png)

        ![計画の最適化](../Step5_最適化/images/9.6.2.png)

    7. 計画値が最適化されたことを確認します。

        ![計画の最適化](../Step5_最適化/images/9.7.png)

10. **利益最大化による計画の最適化**

    1. **2025年** の**RIEKI_PLAN列 ALLセル** を選択し、**Planning**タブ > **・・・** > **Optimize** をクリックします。

        ![計画の最適化](../Step5_最適化/images/10.1.png)

    2. 以下の情報を設定して **Next** をクリックします。
        ※ **Objective** を **Maximize** にすることで、**RIEKI_PLAN** の値が最大になるように最適化します。

        | 項目 | 設定値 |
        |---|---|
        | **Objective** | **Maximize** |
        | **Variables to Update** | **[URIAGE_PLAN]**、**[SHIIREGAKU_PLAN]**、**[YUSOHI_PLAN]** |

        ![計画の最適化](../Step5_最適化/images/10.2.png)

    3. **＋ Add Constraint** をクリックし、以下の情報を設定して **Apply** をクリックします。

        | 項目 | 設定値 |
        |---|---|
        | **Apply to Variable** | **URIAGE_PLAN** |
        | **Set Type** | **Range** |
        | **Min** | **650m** |
        | **Max** | **680m** |

        ![計画の最適化](../Step5_最適化/images/10.3.png)

        ![計画の最適化](../Step5_最適化/images/10.3.2.png)

    4. **＋ Add** をクリックし、以下の情報を設定して **Apply** をクリックします。

        | 項目 | 設定値 |
        |---|---|
        | **Variable** | **SHIIREGAKU_PLAN** |
        | **Set Type** | **Range** |
        | **Min** | **275m** |
        | **Max** | **280m** |

        ![計画の最適化](../Step5_最適化/images/10.4.png)

    5. **＋ Add** をクリックし、以下の情報を設定して **Apply** をクリックします。

        | 項目 | 設定値 |
        |---|---|
        | **Variable** | **YUSOHI_PLAN** |
        | **Set Type** | **Range** |
        | **Min** | **18m** |
        | **Max** | **19m** |

        ![計画の最適化](../Step5_最適化/images/10.5.png)

    6. **Run** をクリックし、目標利益を達成する最適解を確認後、**Apply** をクリックします。

        ![計画の最適化](../Step5_最適化/images/10.6.png)

        ![計画の最適化](../Step5_最適化/images/10.6.2.png)

    7. 計画値が最適化されたことを確認します。

        ![計画の最適化](../Step5_最適化/images/10.7.png)

## Step5 まとめ

以上で、**Step4「最適化」** は完了です。

本ステップでは、以下の作業を実施しました。

- 利益計画シートの作成
- 利益・売上・仕入額・輸送費の計画列の作成
- 目標値に基づく計画の最適化
- 利益最大化による計画の最適化

これにより、売上・仕入額・輸送費に設定した条件をもとに利益計画を最適化し、目標利益の達成に向けた計画や、利益を最大化するための計画を検討できるようになります。

---

# Step6：シナリオ

## 概要

本ステップでは、シナリオ分析用のPlanning Sheetを作成します。

売上増加を想定した楽観的シナリオを作成し、Base Scenarioと比較することで、異なる想定条件による売上への影響を比較・検証します。

## 手順

1. **Planning Sheetの作成**

    1. **Home**タブ > **New Planning Sheet** > 名前に「**SCENARIO**」を入力し、シナリオシートを作成します。

        ![Planning Sheetの作成](../Step6_シナリオ/images/1.1.png)

2. **マトリックスの作成**

    1. データペインからフィールドペインへドラッグアンドドロップし、以下の項目を設定します。

        | 設定項目 | 設定値 |
        |---|---|
        | **Rows** | **05_M_SHOHIN**（**CATEGORY**、**BRAND**、**VARIATION**） |
        | **Columns** | **CALENDAR**（**DATE_Hierarchy**） |
        | **Values** | **MEASURE**（**[ZENNEN_URIAGE]**） |

        ![マトリックスの作成](../Step6_シナリオ/images/2.1.png)

3. **売上予測列の作成**

    1. **Planning**タブ > **Insert Column** > **Copy from another series** > **PY Revenue** > 以下の情報を設定して **Create** をクリックします。

        | 設定項目 | 設定値 |
        |---|---|
        | **Title** | **URIAGE_YOSOKU** |
        | **Insert as** | **Visual Measure** |
        | **Input type** | **Number** |
        | **Column aggregation type** | **Sum** |
        | **Row aggregation type** | **Sum** |
        | **Distribute parent value to children** | **チェックを入れる** |

        ![売上予測列の作成](../Step6_シナリオ/images/3.1.png)

        ![売上予測列の作成](../Step6_シナリオ/images/3.1.2.png)

    2. 「URIAGE_YOSOKU」列が作成されます。

4. **シナリオの作成**

    1. **Model**タブ > **Scenario** > 以下の情報を設定して **Create** をクリックします。

        | 設定項目 | 設定値 |
        |---|---|
        | **Scenario name** | **POSITIVE** |
        | **Include series in scenarios** | **URIAGE_YOSOKU** |

        ![シナリオの作成](../Step6_シナリオ/images/4.1.png)

    2. **2026年** の **雷神エナジー** のスライダーを操作し、シミュレーション値を **5%** に設定します。

        ![シナリオの作成](../Step6_シナリオ/images/4.2.png)

5. **シミュレーション値 入力方法の設定**

    1. **Scenario**タブ > **Input Method** > **Distribution** を選択します。

        ![シミュレーション値 入力方法の設定](../Step6_シナリオ/images/5.1.png)

    2. **2026年** の **匠珈琲** のセルをダブルクリックし、数式バーに **42m** を入力します。

        ![シミュレーション値 入力方法の設定](../Step6_シナリオ/images/5.2.png)

    3. シミュレーション値が反映されたことを確認します。

        ![シミュレーション値 入力方法の設定](../Step6_シナリオ/images/5.3.png)

6. **シナリオの比較**

    1. **Scenario**タブ > **Compare** > 以下の情報を設定します。

        | 設定項目 | 設定値 |
        |---|---|
        | **Compare** | **POSITIVE** |
        | **With** | **Base Scenario** |

        ![シナリオの比較](../Step6_シナリオ/images/6.1.png)

        ![シナリオの比較](../Step6_シナリオ/images/6.1.2.png)

    2. **2026年** に移動し、比較画面を確認します。　※画面上でシミュレーション値を変更することも可能です。

        ![シナリオの比較](../Step6_シナリオ/images/6.2.png)

## Step6 まとめ

以上で、**Step5「シナリオ」** は完了です。

本ステップでは、以下の作業を実施しました。

- シナリオシートの作成
- シナリオの作成
- シナリオの比較

これにより、複数の想定条件による売上への影響を比較・検証し、今後の計画検討に活用できるようになります。


---

# Step7：Writeback

## 概要

本ステップでは、Fabric SQLへの接続を設定し、Planning Sheetで作成した計画データの書き込み先としてSQL DBを設定します。

その後、Writebackを実行し、SQL DBへ計画データを登録します。

## 手順

1. **接続の設定**

    1. **Set up connection** をクリックします。

        ![接続の設定](../Step7_Writeback/images/1.1.png)

    2. **Select a Connection** で **FabricSql_handson**を選択し、**Connect** をクリックします。

        ![接続の設定](../Step7_Writeback/images/1.2.png)

    3. 接続が設定されたことを確認します。

        ![接続の設定](../Step7_Writeback/images/1.3.png)

2. **Writeback宛先の設定**

    1. **YOSAN_KANRI** シートを開き、 **Writeback**タブ > **Add destination** を選択します。

        ![Writeback宛先の設定](../Step7_Writeback/images/2.1.png)

    2. 以下の情報を設定して **Add** をクリックします。

        | 設定項目 | 設定値 |
        |---|---|
        | **Select a Connection** | **FabricSql_handson**|
        | **Select Database From** | **Database Item** |
        | **Database Name** | **DB_name** |
        | **schema** | **dbo** |
        | **Table Name** | **plan_yyyymmdd**（当日の日付に置き換え） |

        ![Writeback宛先の設定](../Step7_Writeback/images/2.2.png)

3. **Writebackの実行**

    1. **Writeback** をクリックし、SQL DBにデータを書き込みます。

        ![Writebackの実行](../Step7_Writeback/images/3.1.png)

    2. Writebackが成功したことを確認します。

        ![Writebackの実行](../Step7_Writeback/images/3.2.png)

4. **SQL DBの確認**

    1. ワークスペース **Plan_workshop**を開き、**DB_name** をクリックします。

        ![SQL DBの確認](../Step7_Writeback/images/4.1.png)

    2. **DB_name** > **dbo** > **テーブル** > **plan_yyyymmdd** をクリックし、データが書き込まれていることを確認します。

        ![SQL DBの確認](../Step7_Writeback/images/4.2.png)
    

## Step7 まとめ

以上で、**Step6「Writeback」** は完了です。

本ステップでは、以下の作業を実施しました。

- Fabric SQL接続の設定
- Writeback宛先の設定
- 計画データのWriteback

これにより、Planning Sheetの計画データを指定したFabric SQLデータベースのテーブルへ書き込みました。


---


