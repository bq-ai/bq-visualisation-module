# BQ AI — Visualisation Module

## Types of Responses

For the MVP phase of the visualisation module, we'll be dealing **exclusively** with the following data types:

1. **standard_text** — for standard text blocks
2. **standard_table** — for standard table blocks
3. **standard_bar_chart** — for standard bar charts
4. **stacked_bar_chart** — for stacked bar charts
5. **double_bar_chart** — for double bar charts
6. **standard_line_chart** — for standard line charts
7. **visualisation_text** — for visualisation text blocks (ALWAYS sent after a chart)

<br />
<br />
<br />

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
        // some response content here
    },
    // ...
    // more data here
]
```

On the client-side of the chatbot, these will be parsed sequentially by the `id` value and streamed to the client. The following sub-headings dictate the format of each individual response type-content pairs to be successfully parsed on the client side:

<br />
<br />
<br />

### standard_text

```JS
const standard_text_example = [
    {
        id: 0,
        response_type: "standard_text",
        response_content: "Cut diamonds, adopted official languages in that they exhibit 'handedness', a distinct. Sleep, set period, egyptians began to spring training.. Absorption or time but may become more advanced, eventually there must be"
    }
]
```

A sample output of this data format looks like:

![text_example](https://i.imgur.com/hp9ZKoX.png)

<br />
<br />
<br />

### standard_table

```JS
const standard_table_example = [
    {
        id: 0,
        response_type: "standard_table",
        response_content: {
            table_heading: "Send the heading of the table here.",
            table_column_headers: ["Company Name", "Total Revenue", ], // all column headers here
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

A sample output of this data format looks like:

![table_example](https://i.imgur.com/xwZzbDl.png)

<br />
<br />
<br />

### standard_bar_chart

```JS
const standard_bar_chart = [
    {
        id: 0,
        response_type: "standard_bar_chart",
        response_content: {
            bar_chart_heading: "Send the heading of the bar chart here.",
            bar_chart_label: "value",
            bar_chart_data: [
                {
                    name: 'Bar Label 01',
                    value: 2400,
                    // note: key MUST match what was sent in bar_chart_label
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

<br />
<br />
<br />

### stacked_bar_chart

```JS
const stacked_bar_chart = [
    {
        id: 0,
        response_type: "stacked_bar_chart",
        response_content: {
            bar_chart_heading: "Send the heading of the bar chart here.",
            bar_chart_labels: ["revenue_in_2022", "revenue_in_2023", ], // these are labels for stack chunks
            bar_chart_data: [
                {
                    name: 'Bar Label 01',
                    revenue_in_2022: 2400,
                    revenue_in_2023: 4000,
                    // note: keys MUST match what was sent in bar_chart_labels
                },
                {
                    name: 'Bar Label 02',
                    revenue_in_2022: 5000,
                    revenue_in_2023: 1000,
                },
                // bars can be added subsequently as required
            ]
        }
    }
]
```

A sample output of this data format looks like:

![bar_chart_example](https://i.imgur.com/U3UbZGu.png)

<br />
<br />
<br />

### double_bar_chart

```JS
const double_bar_chart = [
    {
        id: 0,
        response_type: "double_bar_chart",
        response_content: {
            bar_chart_heading: "Send the heading of the bar chart here.",
            bar_chart_labels: ["revenue_in_2022", "revenue_in_2023"], // send the two labels here
            bar_chart_data: [
                {
                    name: 'Bar Label 01',
                    revenue_in_2022: 2400,
                    revenue_in_2023: 4000,
                    // note: keys MUST match what was sent in bar_chart_labels
                },
                {
                    name: 'Bar Label 02',
                    revenue_in_2022: 5000,
                    revenue_in_2023: 1000,
                },
                // bars can be added subsequently as required
            ]
        }
    }
]
```

A sample output of this data format looks like:

![bar_chart_example](https://i.imgur.com/qKBTCpu.png)

<br />
<br />
<br />

### standard_line_chart

```JS
const standard_line_chart = [
    {
        id: 0,
        response_type: "standard_line_chart",
        response_content: {
            line_chart_heading: "Send the heading of the line chart here.",
            line_chart_label: "value",
            line_chart_data: [
                {
                    name: 'Point 01',
                    value: 2400,
                    // note: key MUST match what was sent in line_chart_label
                },
                {
                    name: 'Point 02',
                    value: 1398,
                },
                {
                    name: 'Point 03',
                    value: 2018,
                },
                // points can be added subsequently as required
            ]
        }
    }
]
```

A sample output of this data format looks like:

![line_chart_example](https://i.imgur.com/XcavRui.png)

<br />
<br />
<br />

### visualisation_text

```JS
const visualisation_text = [
    {
        id: 0,
        response_type: "visualisation_text",
        response_content: "Text content here (but keep it short please)"
    }
]
```

A sample output of this data format looks like: (TODO! — will figure out later)
