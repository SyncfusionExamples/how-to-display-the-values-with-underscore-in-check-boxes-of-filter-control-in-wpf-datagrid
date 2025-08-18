# How to display the values with underscore in check boxes of filter control in wpf datagrid

This example illustrates how to display the values with underscore in check boxes of filter control in [WPF DataGrid](https://www.syncfusion.com/wpf-controls/datagrid)

By default, the check box will not display the first underscore when the check box contains values with underscores. This is the default behavior of the check box.

### Reference links:

https://stackoverflow.com/questions/25310482/wpf-checkbox-content-not-correct

https://stackoverflow.com/questions/4601801/wpf-listbox-skip-underscore-symbols-in-strings

You can allow the check box to display first the underscore when the check box content contains underscore values in filter pop-up window by overriding the CheckBoxFilterControl style.

In, CheckBoxFilterControl style ItemTemplate has been used to load items with check box in filter pop-up. You need to customize this ItemsTemplate to display the underscore value in check box.

### ItemsTemplate Customization

TextBlock has been added to display underscore value in check box. Refer to the following code sample for adding TextBlock in CheckboxFilterControlItemTemplate.

``` xml
<DataTemplate x:Key="CheckboxFilterControlItemTemplate">
    <StackPanel HorizontalAlignment="Stretch" Orientation="Horizontal">
        <CheckBox Margin="4"
                  HorizontalAlignment="Stretch"
                  HorizontalContentAlignment="Stretch"
                  Focusable="False"
                  FontFamily="{Binding FontFamily,RelativeSource={RelativeSource Self}}"
                  FontSize="{Binding FontSize,RelativeSource={RelativeSource Self}}"
                  FontStretch="{Binding FontStretch,RelativeSource={RelativeSource Self}}"
                  FontStyle="{Binding FontStyle,RelativeSource={RelativeSource Self}}"
                  FontWeight="{Binding FontWeight,RelativeSource={RelativeSource Self}}"
                  Foreground="{Binding Foreground,RelativeSource={RelativeSource Self}}"
                  IsChecked="{Binding IsSelected, Mode=TwoWay}" />
        <TextBlock Margin="0,5,0,5" VerticalAlignment="Center" Foreground="Black" Text="{Binding DisplayText, Mode=TwoWay}"/>
    </StackPanel>
</DataTemplate>
```

### Style Customization

``` xml
<Style x:Key="CheckboxFilterControlStyle" TargetType="{x:Type syncfusion:CheckboxFilterControl}">
    <Setter Property="ItemTemplate" Value="{StaticResource CheckboxFilterControlItemTemplate}"/>
    <Setter Property="Template">
        <Setter.Value>
            <ControlTemplate TargetType="{x:Type syncfusion:CheckboxFilterControl}">
                <Grid Height="{TemplateBinding Height}">
                    <Grid.ColumnDefinitions>
                        <ColumnDefinition Width="30" />
                        <ColumnDefinition Width="*" />
                    </Grid.ColumnDefinitions>
 
                    <Border Grid.Column="0"
                        Width="19"
                        Height="19"
                        Margin="4,39,4,4"
                        VerticalAlignment="Top"
                        BorderBrush="#FFB2B2B2"
                        BorderThickness="1,1,1,1"
                        Visibility="{Binding FilteredFrom,
                                    RelativeSource={RelativeSource FindAncestor,
                                    AncestorType={x:Type syncfusion:GridFilterControl}},
                                    Converter={StaticResource filteredFromCheckVisibilityConverter}}">
                        <Path x:Name="PART_FilteredFromCheck1"
                              Width="15"
                              Height="15"
                              Data="M 12.4227,0.00012207C 12.4867,0.126587 12.5333,0.274536 12.6787,0.321411C 9.49199,3.24792 6.704,6.57336 4.69865,10.6827C 4.04399,11.08 3.47066,11.5573 2.83199,11.9706C 2.09467,10.2198 1.692,8.13196 3.8147e-006,7.33606C 0.500004,6.79871 1.31733,6.05994 1.93067,6.2428C 2.85999,6.51868 3.14,7.9054 3.60399,8.81604C 5.80133,5.5387 8.53734,2.19202 12.4227,0.00012207 Z "
                              Fill="Gray"
                              Stretch="Uniform"
                              Visibility="{Binding FilteredFrom,
                                          RelativeSource={RelativeSource FindAncestor,
                                          AncestorType={x:Type syncfusion:GridFilterControl}},
                                          Converter={StaticResource filteredFromCheckVisibilityConverter}}">
                            <Path.RenderTransform>
                                <TransformGroup>
                                    <TransformGroup.Children>
                                        <RotateTransform Angle="0" />
                                        <ScaleTransform ScaleX="1" ScaleY="1" />
                                    </TransformGroup.Children>
                                </TransformGroup>
                            </Path.RenderTransform>
                        </Path>
                    </Border>
 
                    <Grid Grid.Column="1">
                        <Grid.RowDefinitions>
                            <RowDefinition Height="Auto" />
                            <RowDefinition Height="*" />
                        </Grid.RowDefinitions>
 
                        <Grid Margin="0,8,4,2" Background="{TemplateBinding Background}" Visibility="{TemplateBinding SearchOptionVisibility}">
 
                            <TextBox x:Name="PART_SearchTextBox"
                                     Height="25"
                                     HorizontalAlignment="Stretch"
                                     VerticalAlignment="Center"
                                     VerticalContentAlignment="Center"
                                     FontFamily="{TemplateBinding FontFamily}"
                                     FontSize="{TemplateBinding FontSize}"
                                     FontStretch="{TemplateBinding FontWeight}"
                                     FontStyle="{TemplateBinding FontStyle}"
                                     FontWeight="{TemplateBinding FontWeight}"
                                     BorderBrush="#FF727272"
                                     BorderThickness="1" />
 
                            <TextBlock Margin="5,0,0,0"
                                       HorizontalAlignment="Left"
                                       VerticalAlignment="Center"
                                       Foreground="{TemplateBinding Foreground}"
                                       FontFamily="{TemplateBinding FontFamily}"
                                       FontSize="{TemplateBinding FontSize}"
                                       FontStretch="{TemplateBinding FontWeight}"
                                       FontStyle="{TemplateBinding FontStyle}"
                                       FontWeight="{TemplateBinding FontWeight}"
                                       IsHitTestVisible="False"
                                       Opacity="0.7"
                                       Text="{Binding Source={x:Static Member=syncfusion:GridResourceWrapper.Search}}"
                                       Visibility="{TemplateBinding SearchTextBlockVisibility}" />
                            <Border Width="18"
                                    Height="18"
                                    Margin="0,0,5,0"
                                    HorizontalAlignment="Right"
                                    Visibility="{Binding Text,
                                                ElementName=PART_SearchTextBox,
                                                ConverterParameter=searchIcon,
                                                Converter={StaticResource textBlockVisibilityConverter}}">
                                <Path  Fill="Gray"
                                       RenderTransformOrigin="0.5,0.5"
                                       Stretch="Uniform">
                                    <Path.RenderTransform>
                                        <TransformGroup>
                                            <RotateTransform Angle="0" />
                                            <ScaleTransform ScaleX="1" ScaleY="1" />
                                        </TransformGroup>
                                    </Path.RenderTransform>
                                </Path>
                            </Border>
                            <Button x:Name="PART_DeleteButton"
                                    Width="25"
                                    Height="25"
                                    HorizontalAlignment="Right"
                                    VerticalAlignment="Stretch"
                                    Style="{StaticResource deleteBtnStyle}"
                                    FontFamily="{TemplateBinding FontFamily}"
                                    FontSize="{TemplateBinding FontSize}"
                                    FontStretch="{TemplateBinding FontWeight}"
                                    FontStyle="{TemplateBinding FontStyle}"
                                    FontWeight="{TemplateBinding FontWeight}"
                                    Visibility="{Binding Text,
                                    ElementName=PART_SearchTextBox,
                                    ConverterParameter=deletebtn,
                                    Converter={StaticResource textBlockVisibilityConverter}}" />
                        </Grid>
                        <Border Grid.Row="1"
                                Margin="0,4,4,4"
                                BorderBrush="#FFC0C0C0"
                                BorderThickness="1">
                            <Grid>
                                <TextBlock Margin="0,25,0,0"
                                           HorizontalAlignment="Center"
                                           VerticalAlignment="Top"
                                           FontFamily="{TemplateBinding FontFamily}"
                                           FontSize="{TemplateBinding FontSize}"
                                           FontStretch="{TemplateBinding FontWeight}"
                                           FontStyle="{TemplateBinding FontStyle}"
                                           FontWeight="{TemplateBinding FontWeight}"
                                           Text="{Binding Source={x:Static Member=syncfusion:GridResourceWrapper.NoItems}}"
                                           Visibility="{Binding HasItemsSource,
                                                      RelativeSource={RelativeSource TemplatedParent},
                                                      Converter={StaticResource ResourceKey=reverseVisibilityConverter}}" />
                                <Grid Visibility="{Binding HasItemsSource, RelativeSource=   {RelativeSource TemplatedParent}, Converter={StaticResource ResourceKey=boolToVisiblityConverter}}">
                                    <Grid.RowDefinitions>
                                        <RowDefinition Height="Auto" />
                                        <RowDefinition Height="*" />
                                    </Grid.RowDefinitions>
                                    <Grid Grid.Row="1">
                                        <Grid.Resources>
                                            <Storyboard x:Key="LaoadingAnimation" RepeatBehavior="Forever">
                                                <DoubleAnimationUsingKeyFrames Storyboard.TargetName="Path" Storyboard.TargetProperty="(UIElement.RenderTransform).(TransformGroup.Children)[2].(RotateTransform.Angle)">
                                                    <EasingDoubleKeyFrame KeyTime="0" Value="0" />
                                                    <EasingDoubleKeyFrame KeyTime="0:0:5" Value="1170" />
                                                </DoubleAnimationUsingKeyFrames>
                                            </Storyboard>
                                        </Grid.Resources>
                                        <Path x:Name="Path"
                                            Width="26"
                                            Height="26"
                                            Fill="Gray"
                                            RenderTransformOrigin="0.5,0.5"
                                            Stretch="Uniform"
                                            Visibility="{Binding IsItemSourceLoaded,
                                                                Mode=TwoWay,
                                                                RelativeSource={RelativeSource TemplatedParent},
                                                                ConverterParameter={StaticResource LaoadingAnimation},
                                                                Converter={StaticResource ResourceKey=loadingVisiblityConverter}}">
                                            <Path.RenderTransform>
                                                <TransformGroup>
                                                    <ScaleTransform />
                                                    <SkewTransform />
                                                    <RotateTransform />
                                                    <TranslateTransform />
                                                </TransformGroup>
                                            </Path.RenderTransform>
                                        </Path>
                                        <ItemsControl x:Name="PART_ItemsControl"
                                                    Height="{TemplateBinding Height}"
                                                    HorizontalAlignment="Stretch"
                                                    VerticalAlignment="Stretch"
                                                    HorizontalContentAlignment="Stretch"
                                                    VerticalContentAlignment="Stretch"
                                                    ItemTemplate="{TemplateBinding ItemTemplate}"
                                                    ItemsSource="{TemplateBinding ItemsSource}"
                                                    KeyboardNavigation.TabNavigation="Continue"
                                                    Visibility="{Binding IsItemSourceLoaded,
                                                                RelativeSource={RelativeSource TemplatedParent},
                                                                Converter={StaticResource ResourceKey=boolToVisiblityConverter}}">
                                            <ItemsControl.Template>
                                                <ControlTemplate TargetType="{x:Type ItemsControl}">
                                                    <Border Background="{TemplateBinding Background}"
                                                        BorderBrush="{TemplateBinding BorderBrush}"
                                                        Padding="{TemplateBinding Padding}">
                                                        <Grid>
                                                            <ScrollViewer HorizontalAlignment="Stretch"
                                                                        CanContentScroll="True"
                                                                        HorizontalScrollBarVisibility="Auto"
                                                                        Padding="2"
                                                                        SnapsToDevicePixels="true"
                                                                        VerticalScrollBarVisibility="Auto">
                                                                <ItemsPresenter x:Name="PART_ItemsPresenter"
                                                                Margin="{Binding ActualHeight,
                                                                    ElementName=PART_CheckBox, UpdateSourceTrigger=PropertyChanged,
                                                                                                Converter={StaticResource heightToMarginConverter}}"
                                                                ClipToBounds="True"
                                                                Focusable="False" />
                                                            </ScrollViewer>
                                                            <TextBlock Margin="{Binding ElementName=PART_ItemsPresenter,
                                                            Path=Margin}"
                                                                    HorizontalAlignment="Center"
                                                                    VerticalAlignment="Top"
                                                                    Foreground="{TemplateBinding Foreground}"
                                                                    Text="{Binding Source={x:Static Member=syncfusion:GridResourceWrapper.NoMatches}}"
                                                                    Visibility="{Binding ItemsSource,
                                                                                        RelativeSource={RelativeSource TemplatedParent},
                                                                                        ConverterParameter=NoMatchText,
                                                                                        Converter={StaticResource ResourceKey=listItemsVisiblityConverter}}" />
                                                        </Grid>
                                                    </Border>
                                                </ControlTemplate>
                                            </ItemsControl.Template>
                                            <ItemsControl.ItemsPanel>
                                                <ItemsPanelTemplate>
                                                    <VirtualizingStackPanel HorizontalAlignment="Stretch" />
                                                </ItemsPanelTemplate>
                                            </ItemsControl.ItemsPanel>
 
                                        </ItemsControl>
                                    </Grid>
                                    <Border Grid.Row="1"
                                        Margin="0,0,20,0"
                                        VerticalAlignment="Top"
                                        Background="{TemplateBinding Background}"
                                        Visibility="{Binding ItemsSource,
                                                                ElementName=PART_ItemsControl,
                                                                ConverterParameter=ItemsControl,
                                                                Converter={StaticResource ResourceKey=listItemsVisiblityConverter}}">
                                        <CheckBox x:Name="PART_CheckBox"
                                                Margin="10,10,4,4"
                                                HorizontalAlignment="Stretch"
                                                VerticalAlignment="Center"
                                                Content="{Binding Source={x:Static Member=syncfusion:GridResourceWrapper.SelectAll}}"
                                                Focusable="False"
                                                FontFamily="{TemplateBinding FontFamily}"
                                                FontSize="{TemplateBinding FontSize}"
                                                FontStretch="{TemplateBinding FontWeight}"
                                                FontStyle="{TemplateBinding FontStyle}"
                                                FontWeight="{TemplateBinding FontWeight}"
                                                Foreground="{TemplateBinding Foreground}"
                                                IsThreeState="True"
                                                Visibility="{Binding Visibility,
                                                                    ElementName=PART_ItemsControl}" />
                                    </Border>
                                </Grid>
 
                            </Grid>
                        </Border>
                    </Grid>
                </Grid>
            </ControlTemplate>
        </Setter.Value>
    </Setter>
</Style>
<Style BasedOn="{StaticResource CheckboxFilterControlStyle}" TargetType="{x:Type syncfusion:CheckboxFilterControl}" />
```