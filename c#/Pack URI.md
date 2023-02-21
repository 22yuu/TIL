참고한 사이트 [링크](https://devjh.tistory.com/242)

```cs
// pack uri 절대경로 예제 - 이미지 BitMap으로 저장해 Image Control의 Source 속성에 바인딩하는 법
public partial class UserControl_tooltip : UserControl
    {
        public UserControl_tooltip(string imgPath)
        {
            // imgPath : pack://application:,,,/className;component/Resource/ImageFileName.png
            // /className;componet ->를 붙여줘야 해당 클래스를 root로 경로를 탐색함
            InitializeComponent();
            BitmapImage src = new BitmapImage();
            src.BeginInit();
            src.UriSource = new Uri(imgPath, UriKind.Absolute); // UriKind.Relative -> 상대경로
            src.CacheOption = BitmapCacheOption.OnLoad;
            src.EndInit();

            this.Image.Source = src;
        }
    }

```
