# API Management for the AI Era: Leveraging OpenAPI Standards

## [API Days Paris 2025](https://www.apidays.global/events/paris), December 10, 2025

Exercises and Materials for the "API Management for the AI Era: Leveraging OpenAPI Standards" Workshop at the API Days Paris 2025

## Authors / Trainers

- [Erik Wilde](https://github.com/dret)
- [Frank Kilcommins](https://github.com/frankkilcommins/)

### Schedule

#### Part I (14.00-16.00)

- 14.00-14.25: [Overview of APIs and API Business Models](http://dret.net/lectures/api-days-paris-2025/workshop-overview)
- 14.25-14.45: [API Descriptions and OpenAPI](http://dret.net/lectures/api-days-paris-2025/workshop-descriptions)
- 14.45-15.00: Exercise 1 - Designing and Creating an API
- 15.00-15.10: Exercise 2 - Validating OpenAPI
- 15.10-15.30: [API Linting](http://dret.net/lectures/api-days-paris-2025/workshop-linting)
- 15.30-15.45: Exercise 3 - Linting OpenAPI
- 15.45-16.00: [From Developer Experience (DX) to Agent Experience (AX)](http://dret.net/lectures/api-days-paris-2025/workshop-dx-to-ax)

#### Part II (16.30-18.00)

- 16.30-16.50: [Getting your APIs AI-Ready](http://dret.net/lectures/api-days-paris-2025/workshop-api-ai-ready)
- 16.50-17.05: Exercise 4 - Scoring and Improving OpenAPI
- 17.05-17.20: [API Description Pipelines with Overlays](http://dret.net/lectures/api-days-paris-2025/workshop-overlays)
- 17.20-17.30: Exercise 5 - Tweaking OpenAPI
- 17.30-17.45: [AI-Friendly API Workflows with Arazzo](http://dret.net/lectures/api-days-paris-2025/workshop-arazzo)
- 17.45-18.00: Quiz & Certificate

### Slides / Lectures

The slides presented during the workshop are available at [http://dret.net/lectures/api-days-paris-2025/](http://dret.net/lectures/api-days-paris-2025/)

### Tools

The following tools are either required or recommended as part of the exercises:

- [Swagger Editor](https://editor-next.swagger.io/)
- [Scalar](https://editor.scalar.com/)
- [Visual Studio Code](https://code.visualstudio.com/)
- [Spectral](https://github.com/stoplightio/spectral)
- [Spectral VSCode Extension](https://marketplace.visualstudio.com/items?itemName=stoplight.spectral)
- [Overlay Playground](https://overlay.speakeasy.com/)
- [Arazzo Specification GPT](https://chatgpt.com/g/g-673339c216648190a97a5fa3d8258769-arazzo-specification)
- [Arazzo Editor](https://arazzo-editor.symplr.io/)

### Exercise 1

Given the following user story, generate an OpenAPI description to expose endpoints that can satisfy the story requirements:

> Expose endpoints that will allow a user to find the best selling books on the New York Times for the last <number> of days. Allow the details on each book also to be retrieved, things like author, publishedOn, price, trending info, rating. Once a book is known, provide the ability to find locations where the book can be purchased (physical and online). Additionally, there should be an ability to buy a book or list of books.

Options for generation:
1. (preferred) Use an LLM assistant of choice to generate a first pass at the OpenAPI description.
  - Leverage the provided [system-prompt](./system-prompts/openapi-creation-or-modification.md) to set robust guidance for the AI
  - Provide the user story from above or from [user story](./exercise-1/generate-openapi-prompt.md) within exercise 1.
  - Validate the the OpenAPI can render successfully in either [Swagger Editor](https://editor.swagger.io) or [Scalar Editor](https://editor.scalar.com/)
2. (fallback) If you prefer to create manually, the take the skeleton OpenAPI from [exercise-2](./exercise-2/best-selling-skeleton.openapi.yaml) and add in the missing endpoint (with schemas for request and response under `component.schemas`)

### Exercise 2

Let's validate that our APIs have no errors but loading them in either [Swagger Editor](https://editor.swagger.io) or [Scalar Editor](https://editor.scalar.com/).

Fix all issues reported!

### Exercise 3

Now let's lint our API to ensure it passes the core validation rules of OpenAPI using Spectral.

If you need to install Spectral, check our [installation instructions](https://docs.stoplight.io/docs/spectral/b8391e051b7d8-installation).

Lint your API:

```sh
spectral lint best-selling.openapi.yaml --ruleset .spectral.yaml
```

### Exercise 4

Go to Jentic's AI-Readiness Scoring at [https://jentic.com/scorecard](https://jentic.com/scorecard).

1. Now score your API from exercise 3 (you'll need to save it as a YAML or JSON file).
2. Based on the feedback, make alterations to your OpenAPI (you can use Swagger, Scalar, your IDE, or your LLM of choice)
3. Re-score and see if you've improved the score.

Repeat as needed. Can you get to `AI-Ready`?

### Exercise 5

Let's use an overlay to make some changes to our API before publishing. 

Sample changes:
- Update the contact name for the API
- Remove the `/purchase` endpoint and related schemas as we don't want to expose that to public consumers

Take your API and pasted it into the left hand column in [Speakeasy\'s Overlay Playground](https://overlay.speakeasy.com/).
Now get the Overlay file in [exercise-4](./exercise-5/remove-purchase-endpoint.overlay.yaml) and paste it into the Overlay column (right hand side). Review the changes in the central column.

Next steps:
- change the endpoint `/books/best-selling` to `books/best-sellers`
- copy the updated API and verify no linting issues by running it through spectral.