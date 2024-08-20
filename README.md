Hey,

This app was developed as part of a challenge from TRACTIAN, which you can view [here](https://github.com/tractian/challenges/tree/main/mobile).

The goal was to create a Tree View Application that displays company assets, organized by locations, assets, and their associated components.

To populate the tree structure with data, a fake API was used, available [here](https://fake-api.tractian.com). The app retrieves data using GET methods to access companies, their locations, and assets.

Additionally, the design of the app was based on the ([Figma](https://www.figma.com/design/IP50SSLkagXsUNWiZj0PjP/%5BCareers%5D-Flutter-Challenge-v2?node-id=0-1&t=ZxowLpXDFvQxdNks-0)) provided in the challenge's README.

It is possible to check a video demonstrating the app opening for each company and selecting a filter [here](https://drive.google.com/file/d/1hh8Xg6Kr-4ZwatlEhGc6syCU9lTxNKRz/view?usp=sharing).

After successfully completing the challenge and implementing the desired features, it's evident that there are several areas where the application can be further enhanced to improve usability and optimization.

Firstly, I would focus on refining the design of the constructed tree. Currently, the arrangement of locations, assets, and components isn't as clearly hierarchical as a tree structure should be. While I used ExpansionTile to develop the tree nodes and expand their children where applicable in an understandable way, I believe the visual representation could be noticeably better.

Another point for improvement is the separation of dependency setups managed by GetIt. In the current implementation, all dependency injections are configured in the outermost layer of the application. However, some dependencies are only used in more specific, internal layers and features. According to clean architecture principles, these should not be accessible to other features.

Additionally, the RestClient class, which abstracts external service calls using the Dio package for HTTP requests related to the mock API, could be further developed. The class could be enhanced to better handle errors and exceptions, verify authentication (if such logic is required in the future), and generally encapsulate the behavior of a service that retrieves external data.

Moreover, I might need to devise a more optimized and efficient logic for constructing the tree, which is currently in the assets_store.dart file, especially as the volume of data increases.

# NOTE

When searching for locations, assets, or components using a filter, whether by text or sensor type, the search considers the tree structure of the item that matches the filter. From the matching item, the search traverses the tree upwards to locate its 'parents' and displays the tree for those filtered items. For example, if an item has children with the sensor type 'energy' and others with the sensor type 'vibration,' filtering the view by 'energy' will correctly find the matching child. However, when searching for the parent, it displays the entire parent node, including children with the sensor type 'vibration.'

I reflected on this after the implementation and realized I wasn't entirely sure what the expected behavior should be in this situation. However, correcting this would not be difficult, as it could be resolved by simply removing sibling nodes of a different type from the filtered view, ensuring that the view is fully filtered according to the specified criteria.
