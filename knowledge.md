### Validation
- AdornedElementPlaceholder はバリデーション対象のコントロールを表す。
- ex) 従って、以下のように記述するとバリデーション対象のコントロールが赤枠で囲まれるようになる。また、widthとheightは指定しなくても、自動で対象のコントロールサイズに合わせられる。

          <Border BorderBrush="Red" BorderThickness="2" Margin="0,0,6,0">
              <AdornedElementPlaceholder x:Name="_el"/>
          </Border>
