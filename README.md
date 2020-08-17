# The Magical Glyph Reader

In this challenge, you'll launch code that will help you determine the meaning of a Maya glyph using Machine Learning! This is a Vue.js app that runs a local machine learning model trained using [CustomVision.ai](https://customvision.ai), a web-based machine learning tool to train data on pre-trained models.

Because we trained a finite number of glyphs (about 20 of each) on a pre-trained general model which has no understanding of the concept of a glyph, the results are not very conclusive. However, try a few images in the web site produced when running this app and see if you can determine the glyphs "Yax", "Muyal", and "Nah".

This model is testing for the appearance of the three glyphs mentioned above, and should create labeled bounding boxes around identified areas.

Hint: you learned 'Muyal' in Level 1 of the Mystery, 'Yax' in Level 2, and 'Nah' in Level 3. Throughout the [Azure Maya Mystery](https://aka.ms/AzureMayaMystery) you have seen these glyphs and now you know that, together, they form the name of the temple.

> Note, when trying images in this application, be sure to use images sized to 600px wide and 444px high.

Here is the base image to test:

![title glyph][images/title.png]

In the `images` folder you'll find other glyphs to try. Can you discover a pattern?

> Learn how to create this type of app by reading [an article about its architecture](https://dev.to/azure/ice-cream-or-dalmatian-who-can-tell-building-a-machine-learning-powered-pwa-35g7), or by going through its [companion module on Microsoft Learn](https://docs.microsoft.com/learn/modules/create-web-app-with-refreshable-models/?WT.mc_id=mayamystery-github-jelooper)!

---

# Running the Application

## Project setup

```
npm install
```

### Compiles and hot-reloads for development

```
npm run serve
```

# Contributing

This project welcomes contributions and suggestions. Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.opensource.microsoft.com.

When you submit a pull request, a CLA bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., status check, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.

# Legal Notices

Microsoft and any contributors grant you a license to the Microsoft documentation and other content
in this repository under the [Creative Commons Attribution 4.0 International Public License](https://creativecommons.org/licenses/by/4.0/legalcode),
see the [LICENSE](LICENSE) file, and grant you a license to any code in the repository under the [MIT License](https://opensource.org/licenses/MIT), see the
[LICENSE-CODE](LICENSE-CODE) file.

Microsoft, Windows, Microsoft Azure and/or other Microsoft products and services referenced in the documentation
may be either trademarks or registered trademarks of Microsoft in the United States and/or other countries.
The licenses for this project do not grant you rights to use any Microsoft names, logos, or trademarks.
Microsoft's general trademark guidelines can be found at http://go.microsoft.com/fwlink/?LinkID=254653.

Privacy information can be found at https://privacy.microsoft.com/en-us/

Microsoft and any contributors reserve all other rights, whether under their respective copyrights, patents,
or trademarks, whether by implication, estoppel or otherwise.
