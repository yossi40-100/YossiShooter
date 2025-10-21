# Yossi Shooter Template

# Overview
UE5.6のファーストパーソン/サードパーソンテンプレートをもとに、Metal Gear Solid 風のゲームを作っていく公開プロジェクトです。

詳しくはYouTubeとブログで解説予定

Developed with Unreal Engine 5.6


## License
UnrealEngine上でしか使えないアセットを含むため、本リポジトリの内容物もすべてその扱いとなります。

[UE-Only Content - Licensed for Use Only with Unreal Engine-based Products](https://www.unrealengine.com/en-US/eula/content)  


## Contact
YouTubeやブログなどからお願いします。  
For questions, suggestions, or feedback, please contact: https://www.youtube.com/@yossi40-100



## History

### V1.2  2025/10/21
- リターゲットキャラの親BPとして CBP_RetargetBase を追加し、下記の親子関係に  

  - CBP_Base
    - CBP_RetargetBase
       - CBP_PlayerBase
       - CBP_AI_Base


### V1.1 2025/10/21

- 匍匐でのエイムができるようにした
  - 匍匐時はカメラアングルをピッチ⁺10度までしか上げられないように
  - エイムオフセットの入力アングルに90度足して正面の時に真上相当の扱いとした

- Hand-IK調整の仕組みを BP_HandIKSettings に集約
  - レベル上に設置
  - 詳細欄からCharacterを選ぶ
    - エイムして、武器を持って
    - 武器のMuzzleから10mの矢印を伸ばした状態になる
  - 1人称やストレイフモードなどにして、
  - DT for Open 変数などからデータテーブルを開き値を調整する

### V1.0 公開 2025/10/18

- スペースでどこでもトラバーサルシステムを 追加
  - GASP同様にジャンプキー長押しに対応させた
  - [GASP-ALS](https://github.com/PolygonHive/GASP-ALS)のトラバーサルシステムを移植し一部加工
  - アクターコンポーネントに集約し取り外しを簡単にした（プレイヤーだけに実装）
  - TODO: もとからのバグ含め課題がいろいろある
    - 障害物が複数重なっていると計算がうまくいかない
    - 状況によってはキャラクターの方向が地面と水平じゃなくなってしまう
    - 低めのマントル時に大げさすぎる動作
    - 近すぎると一瞬壁に埋もれる

- Fキーでカバーシステム
  - TODO: カバー中も自由に回転できるので壁に埋もれる
  - TBD: しゃがみや伏せでのカバーも欲しい
  - TBD: 完全に飛び出さないで腕だけ的なリーン撃ち


- Qキーでデバッグ用のスローモーション

- Cキーでしゃがみ・しゃがみ歩き・伏せ・匍匐を追加
  - 歩行速度を調整
  - TODO： 匍匐中にエイムすると地面に埋まる


- 1キー・MMB・ALTでカメラ視点切り替えの追加
  - 3人称のときストレイフOn/Offでカメラを近づける
  - ALTキーで3人称視点の左右切り替え


- リターゲットキャラ用のABP_GenericRetargetを追加
  - 例示のため、（本来は必要ないけど、）QuinnからMannyへのRTG_QuinnToMannyを作成しCBP_PlayerBaseとCBP_AI_Baseに設定


- ハンドIK
  - データテーブル DT_HandIK_Player などにハンドIK用のオフセット情報を分離できるようにした
  - TODO: IK補正値の調整が面倒（仮で、CBP_BaseのBeginPlayに接続すると調整できる処理をおいてある）
  - TODO: 右手の持ち手ソケット位置補正と左手しか補正していない


 - 武器の種類として素手 Unarmed を追加した （今時点は何も持たないってだけ）


- 敵と操作キャラを共通の CBP_Base から派生させ、重複する部分の大半を親に移動した
  - AIはカメラなし、AIコントローラでステートツリー制御
  - プレイヤーはカメラあり、トラバーサルシステムあり

### V0.1
- UE5.6.1の弾の作り替えを取り込み　ついでにもとのグレランの跳ねる球を残して使えるようにしてみた
  - DT_WeaponListに登録して、それを飛ばせる武器として
  - BP_Weapon_GrenadeLauncher_1 を元のやつの子クラスとして追加

- UE5.6.1のダメージ時に外枠が黄色く光る演出を取り込み

- プロジェクタイルのコリジョンがカメラを無視してくれないため頻繁にクリップするのを改善
  - Projectileのコリジョン設定でCameraをIgnoreにするだけではダメで、ぶつかった後PhysicsActorに変化しているのでそれもCameraをIgnoreにした
  - 副作用としてもともとPhysicsActorなキューブなどもCameraが回り込まなくなる


- 歩きと走りのブレンドスペースを更新 UE5.6.1のテンプレートの更新を取入れ
  - まだ少しぎこちない感はあるけど、歩けるようになった


- UE5.6 の ファーストパーソン アリーナシューター テンプレートをもとに、初心者向けでない要素をある程度削減して簡単化した
  - コントロールリグなどをいったん削除、武器毎に分かれていたABPを共通化
