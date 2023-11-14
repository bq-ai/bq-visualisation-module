# BQ AI — Visualisation Module

## Types of Responses

For the MVP phase of the visualisation module, we'll be dealing **exclusively** with the following data types:

- **standard_text** — for standard text blocks
- **standard_table** — for standard table blocks
- **standard_bar_chart** — for standard bar charts
- **stacked_bar_chart** — for stacked bar charts
- **double_bar_chart** — for double bar charts
- **standard_line_chart** — for standard line charts
- **visualisation_text** — for visualisation text blocks (paired w/ a chart)

## Schema for Response Structures

Overall, the response from LLM-02 should return an array that essentially represents a stream of sequential type-content pairs in a format represented by:

```JavaScript
const response = [
    {
        id: 0,
        response_type: "standard_text",
        response_content: "Proident laboris commodo cupidatat ipsum sint est nisi labore culpa eu irure adipisicing ut duis."
    },
    {
        id: 1,
        response_type: "standard_bar_chart",
        response_content: [
            // some chart data here
        ]
    },
    // ...
    // more data here
]
```

On the client-side of the chatbot, these will be parsed sequentially by the `id` value and streamed to the client. The following sub-headings dictate the format of each individual response type-content pairs to be successfully parsed on the client side:

### standard_text

```JS
const standard_text_example = [
    {
        id: 0,
        response_type: "standard_text",
        response_content: "Text content can be sent in a markdown format here."
    }
]
```

### standard_table

```JS
const standard_table_example = [
    {
        id: 0,
        response_type: "standard_table",
        response_content: {
            table_heading: "Send the heading of the table here.",
            table_column_headers: ["Company Name", "Total Revenue", ] // all column headers here
            table_data: [
                ["Apple", "INR 20Cr", ],
                ["Microsoft", "INR 50Cr", ],
                ["Google", "INR 6Cr", ],
                // all entries as arrays
            ]
        }
    }
]
```

### standard_bar_chart

```JS
const standard_bar_chart = [
    {
        id: 0,
        response_type: "standard_bar_chart",
        response_content: {
            bar_chart_heading: "Send the heading of the bar chart here.",
            bar_chart_data: [
                {
                    name: 'Bar Label 01',
                    value: 2400,
                },
                {
                    name: 'Bar Label 02',
                    value: 1398,
                },
                // bars can be added subsequently as required
            ]
        }
    }
]
```

A sample output of this data format looks like:

![bar_chart_example](https://i.imgur.com/8Y98rw6.png)
