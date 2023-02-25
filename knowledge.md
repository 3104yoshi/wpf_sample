### Validation
- 参考 https://learn.microsoft.com/en-us/archive/msdn-magazine/2010/june/msdn-magazine-input-validation-enforcing-complex-business-data-rules-with-wpf
- バリデーションの手順
1. プロパティに制約をつける
2. プロパティのバリデーションを行う
3. バインディング時に System.Windows.Data.Binding.ValidatesOnExceptions プロパティをTrueにする
4. Validation の結果に応じた処理を追加する

#### 1. プロパティに制約をつける方法
- System.ComponentModel.DataAnnotations 以下のアノテーションを設定することでプロパティに制約を付加できる
- ex)以下は、10文字までかつ、半角数字のみ、という制約を付けた例
``` C#
        [MaxLength(10, ErrorMessage = "10文字までしか入力できません")]
        [RegularExpression(@"^[0-9]+$", ErrorMessage ="半角数字以外は入力できません")]
        public string Text
        {
            get { return _text; }
            set { ValidateProperty(value, nameof(this.Text));
                SetProperty(ref _text, value); }
        }
```

#### Validationチェック時に対象のコントロールを変化させたい場合 (赤枠で囲む、文字の色を変える、など)
- AdornedElementPlaceholder はバリデーション対象のコントロールを表す。
- ex) 従って、以下のように記述するとバリデーション対象のコントロールが赤枠で囲まれるようになる。また、widthとheightは指定しなくても、自動で対象のコントロールサイズに合わせられる。

          <Border BorderBrush="Red" BorderThickness="2" Margin="0,0,6,0">
              <AdornedElementPlaceholder x:Name="_el"/>
          </Border>
