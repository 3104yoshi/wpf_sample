# Validation
- 参考 https://learn.microsoft.com/en-us/archive/msdn-magazine/2010/june/msdn-magazine-input-validation-enforcing-complex-business-data-rules-with-wpf
- バリデーションの手順
1. プロパティのバリデーションを行う (アノテーションとValidator を組み合わせる方法、ValidationRule を実装する方法の2つある)
1. バインディング時に System.Windows.Data.Binding.ValidatesOnExceptions プロパティをTrueにする
1. Validation の結果に応じた処理を追加する

## プロパティのバリデーション方法
### アノテーションとValidator を組み合わせる方法
##### アノテーションをつける(制約)
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
