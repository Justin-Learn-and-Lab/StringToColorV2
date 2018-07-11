# StringToColor 第二版

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;

namespace StringToColor
{
	public class StringToColor
	{
		public Color Transfer(string name)
		{
			Color color;
			ColorFactory factory = new ColorFactory(name);
			color = factory.GetColor();

			if (color == Color.Empty)
				throw new ArgumentException("不正確的顏色名稱");
			else
				return color;
		}
	}

	public class ColorFactory
	{
		private string colorName;

		private List<ColorManagement.IColor> colors;

		public ColorFactory(string name)
		{
			colorName = name;
			colors = ColorManagement.RegistereColor();
		}

		public Color GetColor()
		{
			foreach (var item in colors)
			{
				if (item.GetType().Name.ToLower() == colorName.ToLower())
				{
					return item.GetColor();
				}
			}

			return Color.Empty;
		}
	}

	public class ColorManagement
	{
		public interface IColor
		{
			Color GetColor();
		}

		public static List<IColor> RegistereColor()
		{
			List<IColor> colors = new List<IColor>();

			colors.Add(new Red());
			colors.Add(new Green());
			colors.Add(new Blue());

			return colors;
		}

		public class Red : IColor
		{
			public Color GetColor()
			{
				return Color.FromArgb(0xFF, 0xFF, 0x00, 0x00);
			}
		}

		public class Green : IColor
		{
			public Color GetColor()
			{
				return Color.FromArgb(0xFF, 0x00, 0xFF, 0x00);
			}
		}

		public class Blue : IColor
		{
			public Color GetColor()
			{
				return Color.FromArgb(0xFF, 0x00, 0x00, 0xFF);
			}
		}
	}
}
```

上一版仍有違反單一責任原則

在Transfer方法當中有
1.註冊顏色
2.顏色判別
3.回傳顏色

共3個行為，因此分解出來

ColorManagement負責註冊顏色

ColorFactory負責進行產出Color

符合了單一責任原則
