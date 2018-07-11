# 『SOLID 重構挑戰練習』

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

		private List<IColor> colors;

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
		public static List<IColor> RegistereColor()
		{
			List<IColor> colors = new List<IColor>();

			colors.Add(new Red());
			colors.Add(new Green());
			colors.Add(new Blue());

			return colors;
		}
	}

	public interface IColor
	{
		Color GetColor();
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
```

Transfer的方法只負責傳送name，然後接收ColorFactory的結果
