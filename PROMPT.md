# BQ AI — Visualisation Module

## General Schema for Response Structures

Overall, the response from LLM-02 should return three things:

1. An array that essentially represents a stream of sequential type-content pairs
2. A generated summary of the user's question and the answer generated by the model
3. Related questions that user might want to ask as follow up question

```JavaScript
const LLM02_JSON_MODEL_RESPONSE = {
    data = [
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
    ],
    generated_summary: "Summary of the question-answer conversation here",
    related_questions: [
        "Question 01",
        "Question 02",
    ]
}
```

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

## An Example of a Final Compounded Query

```JS
const LLM02_JSON_MODEL_RESPONSE = {
    data = [
        {
            id: 0,
            response_type: "standard_text",
            response_content: "Proident laboris commodo cupidatat ipsum sint est nisi labore culpa eu irure adipisicing ut duis."
        },
        {
            id: 1,
            response_type: "standard_table",
            response_content: {
                table_heading: "Send the heading of the table here.",
                table_column_headers: ["Company Name", "Total Revenue", ],
                table_data: [
                    ["Apple", "INR 20Cr", ],
                    ["Microsoft", "INR 50Cr", ],
                    ["Google", "INR 6Cr", ],
                ]
            }
        },
        {
            id: 2,
            response_type: "visualisation_text",
            response_content: "Text content here (but keep it short please)"
        },
        {
            id: 3,
            response_type: "double_bar_chart",
            response_content: {
                bar_chart_heading: "Send the heading of the bar chart here.",
                bar_chart_labels: ["revenue_in_2022", "revenue_in_2023"],
                bar_chart_data: [
                    {
                        name: 'Bar Label 01',
                        revenue_in_2022: 2400,
                        revenue_in_2023: 4000,
                    },
                    {
                        name: 'Bar Label 02',
                        revenue_in_2022: 5000,
                        revenue_in_2023: 1000,
                    },
                ]
            }
        },
        {
            id: 4,
            response_type: "visualisation_text",
            response_content: "Text content here (but keep it short please)"
        },
        // ...
        // so on and so forth
    ],
    generated_summary: "",
    related_questions: [
        "Question 01",
        "Question 02",
    ]
}

```
