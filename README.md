```markdown
# SEC Entity Shares Outstanding Viewer

## Summary

This application provides a dynamic and interactive view of "Entity Common Stock Shares Outstanding" data, directly fetched from the U.S. Securities and Exchange Commission (SEC) EDGAR API. It processes the financial data to identify and display the maximum and minimum shares outstanding values, along with their corresponding fiscal years, specifically focusing on data from 2021 onwards.

The application is initially configured to display data for Citigroup (CIK 0000831001). A key feature is its ability to dynamically update the displayed information for any other SEC-listed company by simply providing its Central Index Key (CIK) via a URL parameter, all without requiring a page reload.

## Setup Instructions

To run this application, no special setup or server environment is required.

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/your-username/your-repo-name.git
    cd your-repo-name
    ```
2.  **Open `index.html`:** Simply open the `index.html` file in your preferred web browser.

### Viewing Data for Other Companies

To view data for a different company, append a `?CIK=` parameter with the 10-digit CIK to the `index.html` URL in your browser's address bar. For example:

`file:///path/to/your/repo/index.html?CIK=0001018724`

The page will automatically fetch and display the shares outstanding data for the new CIK without a full page reload.

## Code Explanation

The project is structured with the following key components:

*   **`index.html`**: This is the primary user interface of the application. It contains the HTML structure responsible for displaying the company name, and the maximum and minimum common stock shares outstanding figures along with their respective fiscal years. Embedded JavaScript within this file handles:
    *   **Data Fetching**: Making requests to the SEC EDGAR API (or a proxy like AIPipe for dynamic CIK requests) to retrieve `EntityCommonStockSharesOutstanding` data. It strictly adheres to SEC guidance by including a descriptive `User-Agent` header for API calls.
    *   **Data Processing**: Parsing the JSON response, filtering entries where `fy` (fiscal year) is greater than "2020" and `val` is a numeric value.
    *   **Calculation**: Determining the highest (`max`) and lowest (`min`) `val` and their corresponding `fy` from the filtered data.
    *   **Dynamic Rendering**: Updating the HTML elements on the page, including the `<title>`, `<h1>`, `share-entity-name`, `share-max-value`, `share-max-fy`, `share-min-value`, and `share-min-fy` IDs. This is performed seamlessly without a page reload when a CIK parameter is detected in the URL.
*   **`data.json`**: This file stores the pre-processed shares outstanding data (entity name, max value/fy, min value/fy) for the default company, Citigroup (CIK 0000831001). It serves as the initial data source when `index.html` is opened without a specific CIK URL parameter.
*   **`uid.txt`**: A static text file included in the repository as per project requirements.

The client-side JavaScript in `index.html` orchestrates the entire process, providing a responsive and interactive experience for exploring SEC financial data.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
```