# How-to-use-font-awesome-icons-in-.net-MAUI-SfAccordion

This article illustrates how to use font awesome icons in [.NET MAUI SfAccordion](https://www.syncfusion.com/maui-controls/maui-accordion).

In .NET MAUI, you can seamlessly use these icons within the SfAccordion control to create visually rich and interactive list items.

By following the steps below, you’ll learn how to:

STEP 1: Download the font icons on [FontAwesome](https://www.cdnpkg.com/font-awesome/file/fa-solid-900.ttf/). 
STEP 2: Add the downloaded font file in Resouces->Fonts folder.
STEP 3: Register the font in MauiProgram.cs file.
STEP 4: Update the xaml file

**XAML:**
 ```xml
<ContentPage.Resources>
    <ResourceDictionary>
        <x:String x:Key="FontAwesome">FASolid</x:String>
    </ResourceDictionary>
</ContentPage.Resources>

<accordion:SfAccordion x:Name="accordion" BindableLayout.ItemsSource="{Binding Info}" ExpandMode="SingleOrNone" HeaderIconPosition="Start">
    <BindableLayout.ItemTemplate>
        <DataTemplate>
            <accordion:AccordionItem >
                <accordion:AccordionItem.Header>
                    <Grid>
                        <Label TextColor="#495F6E" Text="{Binding Name}" VerticalOptions="Center" HorizontalOptions="StartAndExpand" HeightRequest="50" VerticalTextAlignment="Center"/>
                        <Button Grid.Column="1" HeightRequest="50" WidthRequest="50"
                                Command="{Binding Path=BindingContext.FavouriteCommand, Source={x:Reference accordion}}"
                                CommandParameter="{Binding .}" BackgroundColor="Transparent">
                            <Button.ImageSource>
                                <FontImageSource Glyph="{Binding FavouriteIcon}" FontFamily="{StaticResource FontAwesome}"
                                                 Color="#ea2c62" Size="18" />
                            </Button.ImageSource>
                        </Button>
                    </Grid>
                </accordion:AccordionItem.Header>
                <accordion:AccordionItem.Content>
                    <Grid BackgroundColor="#e8e8e8" Padding="5,0,0,0">
                        <Label Text="{Binding Description}" VerticalOptions="Center"/>
                    </Grid>
                </accordion:AccordionItem.Content>
            </accordion:AccordionItem>
        </DataTemplate>
    </BindableLayout.ItemTemplate>
</accordion:SfAccordion>
 ```

 STEP 5: Define different unicode values for each item.

**ViewModel**
```csharp
public class ItemInfoRepository
{
    #region Properties
    public ObservableCollection<ItemInfo> Info { get; set; }
    public Command<object> FavouriteCommand { get; set; }
    #endregion

    #region Constructor
    public ItemInfoRepository()
    {
        FavouriteCommand = new Command<object>(OnFavouriteClicked);

        Info = new ObservableCollection<ItemInfo>();
        Info.Add(new ItemInfo() { Name = "Cheese burger", Description = "Hamburger accompanied with melted cheese. The term itself is a portmanteau of the words cheese and hamburger. The cheese is usually sliced, then added a short time before the hamburger finishes cooking to allow it to melt.", FavouriteIcon = "\uf004" });
        Info.Add(new ItemInfo() { Name = "Veggie burger", Description = "Veggie burger, garden burger, or tofu burger uses a meat analogue, a meat substitute such as tofu, textured vegetable protein, seitan (wheat gluten), Quorn, beans, grains or an assortment of vegetables, which are ground up and formed into patties.",  FavouriteIcon = "\uf0f4" });
        Info.Add(new ItemInfo() { Name = "Barbecue burger", Description = "Prepared with ground beef, mixed with onions and barbecue sauce, and then grilled. Once the meat has been turned once, barbecue sauce is spread on top and grilled until the sauce caramelizes.", FavouriteIcon = "\uf816" });
        Info.Add(new ItemInfo() { Name = "Chili burger", Description = "Consists of a hamburger, with the patty topped with chili con carne.", FavouriteIcon = "\uf005" });
    }
    #endregion

    #region Methods
    private void OnFavouriteClicked(object obj)
    {
        var item = obj as ItemInfo;
        item.FavouriteIcon = item.FavouriteIcon == "\uf005" ? "\uf004" : "\uf005";
    }
    #endregion
}
```

Download the complete sample from [GitHub](https://github.com/SyncfusionExamples/How-to-use-font-awesome-icons-in-.net-MAUI-SfAccordion/tree/master)