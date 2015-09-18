`T4Resx` allows developers to quickly gain access to the key names in their Resource files -- something that can be useful in eliminating magic strings in cases where type awareness or localization are desired.

Take, for instance, the following MVC model class. It is localizable because it pulls its display values from a resource file. It also contains ZERO magic strings (although they still exist somewhere -- they have to -- but they are isolated in one location, where they belong). This file was created after `T4Resx.CSharp` was installed to the project.

```
using System.ComponentModel.DataAnnotations;

using MvcApplication1.Properties;

using res = MvcApplication1.ResourceKeys.Resources;

namespace MvcApplication1.Models.Account
{
	public class LoginAttempt
	{
		[Display(ResourceType = typeof (Resources), Name = res.UserNameLabel)]
		[Required(ErrorMessageResourceType = typeof (Resources), ErrorMessageResourceName = res.UserNameRequired)]
		public string UserName{ get; set; }

		[DataType(DataType.Password)]
		[Display(ResourceType = typeof (Resources), Name = res.PasswordLabel)]
		[Required(ErrorMessageResourceType = typeof (Resources), ErrorMessageResourceName = res.PasswordRequired)]
		public string Password{ get; set; }

		[Display(ResourceType = typeof (Resources), Name = res.RememberLoginLabel)]
		public bool RememberLogin{ get; set; }
	}
}
```

Whenever you add, rename, or delete an entry from one of your resource files, simply right click the `T4Resx.tt` file in Solution Explorer or Solution Navigator, and select "Run Custom Tool". This will cause the T4 template to run, re-generating the wrapper class with up-to-date entries. As an alternative (a great one) to doing this manually, you can have your T4 template auto-run on every build by using [Chirpy](http://chirpy.codeplex.com/).

Enjoy!