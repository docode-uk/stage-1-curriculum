# How to run the project locally

This project uses Gitbook to generate the book that can be visualised in a browser. To run the project locally, you need to have Gitbook installed on your machine. If you don't have Gitbook installed, you can install it by running the following command:

```bash
npm install @gitbook-ng/gitbook
```

Once you have Gitbook installed, you can run the following commands to start the project:

```bash
cd book
npx gitbook serve
```

This will start a local server that will serve the book on `http://localhost:4000`. You can now open your browser and navigate to `http://localhost:4000` to view the book.

# How to include new content
Inside the `book` directory, you will find a number of directories that represent the different chapters of the book. Each chapter has its own README.md file that an overview of the content of the chapter, and is the landing page for that chapter. Inside each chapter directory, you will find the content of the chapter split into multiple markdown files.

The `SUMMARY.md` file in the `book` directory is the file that Gitbook uses to generate the order of the chapters and the table of contents of the book. If you want to add a new chapter to the book, you will need to add a new entry to the `SUMMARY.md` file. 

We can consider adding a `SUMMARY.md` file to each chapter directory to make it easier to navigate the book once the chapters get bigger. For now, we do the ordering in the main `book/SUMMARY.md` file.