# Quiznuxt

Simple quiz app for Nuxt3 learning and college exam questions (current question database is not correct and only sample) <br /> <br/>
Available at https://nom-tau.vercel.app/

![Sample quiz question](https://i.imgur.com/Xak30C2.png)

To add your own database replace the file `/public/questions.json` with your own json file. <br />
The JSON structure you need to maintain:
```json
 {
    "question": "Question title here!",
    "answers": [
        "good answer",
        "bad answer",
        "bad answer",
        "bad answer", 
        "bad answer"
    ]
}
```
### TO DO:
- a new mode that repeats at the end the questions we answered wrong
- multiple choice
- different grading modes, negative points etc.

## Setup

Make sure to install the dependencies

```bash
yarn install
```

## Development

Start the development server on http://localhost:3000

```bash
yarn dev
```

## Production

Build the application for production:

```bash
yarn build
```

Checkout the [deployment documentation](https://v3.nuxtjs.org/docs/deployment).