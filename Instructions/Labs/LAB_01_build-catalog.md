---
lab:
  title: 'ラボ 1: エンタイトルメントで使用するカタログの作成'
  module: 'Module : Deploying access using Microsoft Entra entitlement management'
---

# ラボ 1: Microsoft Entra エンタイトルメント管理でカタログを作成する

## ラボのシナリオ

ある中規模のソフトウェア開発会社で、IT 部門はエンタイトルメント管理のために Microsoft Entra を実装することにしました。 主な目標は、組織全体のリソースとアプリケーションへのアクセスを合理化することです。 Microsoft Entra では、ロールまたはプロジェクトに基づいてアクセス パッケージを定義できるため、アクセス権の付与または取り消しのプロセスが簡略化されます。 たとえば、新しい開発者がプロジェクトに参加した場合、IT 部門は、対応するアクセス パッケージに割り当てることで、必要なアクセス権をその開発者に簡単に付与できます。 この結果、時間を節約できるだけでなく、不正アクセスのリスクも軽減されます。 さらに、Microsoft Entra の定期的なアクセス レビューにより、適切なユーザーのみが機密リソースにアクセスできるようになります。 実装ラボでは、IT チームがさまざまなアクセス パッケージを設定し、自動のアクセス権割り当てとアクセス権失効のポリシーを定義し、模擬のアクセス レビューを実施します。

## 目標

このラボを完了すると、次のことができるようになります。

- カタログを作成します。
- アクセス パッケージを構成します。
- アクセス パッケージをユーザーにデプロイします。
- エンタイトルメントをユーザーとして受け入れ、リソース アクセスを確認します。
- パッケージへのアクセスを取り消します。

## ラボのセットアップ
  - **推定時間**:30 分

### 演習 1: 営業チームのカタログを作成する

#### タスク 1: カタログを作成する

1. Microsoft Entra 管理センター (`https://Entra.Microsoft.com`) を起動します。

1. 左側のメニューで、**[ID ガバナンス]**、**[エンタイトルメント管理]** の順に移動します。

1. メニューから **[カタログ]** を選択します。

 ![[新しいカタログ] ボタンが強調表示されている [新しいカタログの作成] 画面のスクリーンショット。  名前、説明、"有効" のフィールドがあります。](./Media/create-new-catalog.png)

1. 画面の上部で **[+ 新しいカタログ]** を選択します。

1. 次の値を使用して、**新しいカタログ**の名前と説明を設定します。

  | フィールド | 値 |
  | :---  | :---  |
  | 名前  | `catSales` |
  | 説明 | `Use this catalog to assign resources for memebers of the Sales team.` |
  | Enabled | はい |
  | 外部ユーザーに有効 | いいえ |
  | | |

1. **［作成］** を選択します

#### タスク 2: カタログにリソースを追加する

1. まだ開いていない場合は、**Microsoft Entra 管理センター**、**[ID ガバナンス]**、**[エンタイトルメント管理]**、**[カタログ]** ページの順に移動します。

1. 前のタスクで作成した **[catSales]** を選択します。

1. メニューから **[リソース]** を選択します。

1. 次に、ページの上部で **[+ リソースの追加]** を選択します。

 ![カタログ ユーザー インターフェイスへのリソースの追加のスクリーンショット。 Teams、アプリケーション、SharePoint などのアイテムを追加できます。](./Media/add-resources-to-catalog.png)

1. 画面の上部にあるセレクターを使用して、次のリソースを追加します。

  | リソースの種類 | Value |
  | :---  | :---  |
  | + グループとチーム  | 営業とマーケティング、米国営業 |
  | + アプリケーション | LinkedIn |
  | + SharePoint サイト | 営業とマーケティング、米国営業 |
  | | |

1. **追加** ボタンを選択します。

#### タスク 3: エンタイトルメントを受け取る新しいユーザーを作成する

1. まだ開いていない場合は、**Microsoft Entra 管理センター**にアクセスします。

1. 左側のメニューで、メニューから **[ID]**、**[ユーザー]**、**[すべてのユーザー]** の順に選択します。

1. ページの上部にある **[+ 新しいユーザー]** を選択します。

1. **[基本]** ページで以下の値を入力します。

  | フィールド | 値 |
  | :---  | :---  |
  | ユーザー プリンシパル名  | `ChrisGr` |
  | 表示名 | `Christopher Green` |
  | 自動生成されたパスワード | オン |
  | Account enabled | オン |
  | | |

1. "パスワード" をコピーしてメモ帳などの安全な場所に貼り付けます (このラボの後半でパスワードが必要になります)。

1. [プロパティ] タブを選択します。

1. [プロパティ] 画面の下部で、**[利用場所] を [米国]** に設定します。

1. **[確認および作成]**、**[作成]** の順に選択します。

#### タスク 4: アクセス パッケージを生成する

1. Microsoft Entra 管理センターで、**[ID ガバナンス]**、**[エンタイトルメント管理]** の順に選択します。

1. [エンタイトルメント管理] メニューから **[アクセス パッケージ]** を選択します。

1. 画面の上部にある **[+ 新しいアクセス パッケージ]** を選択します。

1. 要求された値を入力します。

  | フィールド | 値 |
  | :---  | :---  |
  | 名前  | `pckSales` |
  | 表示名 | `Use this access package to assign resources to members of the Sales team.` |
  | カタログ | catSales |
  | | |

  **注** - 前のタスクで作成した catSales カタログを選択する必要があります。 そうすることで、このパッケージで割り当てることができるリソースの一覧が表示されます。  既定として一覧表示される一般パッケージがあります。  誤ってこれを選択した場合、使用可能なリソースは表示されません。

1. [リソース ロール] タブを選択します。

1. catSales カタログの項目から、対象ユーザーのアクセス パッケージに指定するリソースを選択します。 次に、**[ロールの選択]** ドロップダウンを使用して、ロールを次の表のように設定します。

  | リソースの種類 | Value | ロール |
  | :---  | :---  | :--- |
  | + グループとチーム  | 営業とマーケティング | メンバー |
  | + アプリケーション | LinkedIn | msiam_access |
  | + SharePoint サイト | 米国営業 | 米国営業メンバー |
  | | |

1. **[ロールの選択]** ドロップダウンを設定して、各項目のロールを **[メンバー]** に設定します。

1. **[次へ: 要求]** を使用して [要求] タブに進みます。

1. **[アクセス権を要求できるユーザー]** で、オプション **[なし (管理者直接割り当てのみ)] を選択します。

1. **[有効にする]** を **[はい]** に設定します。

1. 画面の上部にあるラベルを使用して、**[ライフサイクル]** タブに移動します。

1. 値を選択してパッケージのライフサイクルを設定します。

  | フィールド | 値 |
  | :---  | :---  |
  | アクセス パッケージの割り当てに有効期限を設ける  | 日数 |
  | 割り当ての期限切れまでの期間 | 30 |
  | ユーザーは特定のタイムラインを要求できる | いいえ |
  | アクセス レビューを要求する | いいえ |
  | | |

1. 画面の下部にある **[確認および作成]** を選択します。

1. [確認および作成] 画面で選択した値を確認します。

1. **[作成]** を選択してアクセス パッケージを作成します。

#### タスク 5: パッケージを Christopher に割り当てる

1. **Microsoft Entra 管理センター**、**[ID ガバナンス]**、**[エンタイトルメント管理]** の順に移動し、**[アクセス パッケージ]** メニューを開きます。

1. 前のタスクで作成した **[pckSales]** を選択します。

1. メニューで **[割り当て]** を選択します。

1. 画面の上部で **[+ 新しい割り当て]** を選択します。

1. **[ポリシーの選択]** には、ドロップダウンで指定した**初期ポリシー**を使用します。

1. **既に自分のディレクトリにいるユーザー**にマークが付いていることを確認します。

1. ダイアログから **[ユーザーの追加]** 項目を選択します。

1. ユーザーの一覧で **Christopher Green** を探します。  その名前の横にあるボックスにチェックを入れます。  そして、画面の下部にある **[選択]** ボタンを選択します。

1. 他の値については既定値に設定されたままにします。

1. ページの下部にある **[追加]** ボタンを選びます。

#### タスク 6: Christopher Green が追加されたかどうか確認する

1. ブラウザーで**新しい InPrivate ウィンドウ**を開きます。

1. **Microsoft Entra 管理センター** (アドレスは `https://entra.microsoft.com`) に接続します。

1. 以前に作成した Chistopher Green のアカウントとパスワードを使用してサイトにログインします。

1. パスワードの変更を求められます。  新しいパスワードを設定し、後で使用するためにメモ帳などのツールで記録します。

1. **[ID]**、**[ユーザー]**、**[すべてのユーザー]** の順に選択し、**[Christopher Green]** を選択します。

1. 左側のメニューで **[グループ]** を選択します。

1. アクセス パッケージごとに、**[営業とマーケティング]** グループにアクセス権が付与されていることを確認します。

1. 左側のメニューで **[アプリケーション]** を選択します。

1. **LinkedIn** が割り当てられているアプリケーションになっていることを確認します。

#### タスク 7: チャレンジ - アクセス パッケージに対する動的な変更

  **注** - このタスクにはステップ バイ ステップの手順はありません。 一連のタスクが用意されており、上記のこれまでの手順を参照することで、特定の変更を行う箇所を思い出すことができます。

- **Microsoft Entra 管理センター**に管理者アカウントでログインします。
- **pckSales** アクセス パッケージを開きます。
- **[リソース ロール]** に移動して、**[営業とマーケティング]** グループを削除し、代わりに **[米国営業]** グループを追加します。
- **[割り当て]** タブを使用して、割り当てを**再処理**します。
- ログアウトし、Christopher Green としてまたログインします。  グループの割り当てが変更されていることに注意してください。  速くて簡単です。
- Christopher Green の割り当てを削除して、アクセス権を取り消します。

### まとめ
これは、エンタイトルメント管理の基本的な機能のデモをする簡単なラボです。  この機能を使用できるオプションと、ラボ内で構成できる高度な構成オプションについて考えてみましょう。