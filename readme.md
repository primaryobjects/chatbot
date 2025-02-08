Chatbot using Retrieval Augmented Generation and LLM
====================================================

A chatbot that uses a private knowledge-base with retrieval augmented generation.

https://generativeai.pub/how-i-built-my-own-ai-chatbot-and-you-can-too-b1a9c9e4b39c

## What is it?

This is an easy [tutorial](chatbot.ipynb) for creating a basic chatbot with a private knowledge-base. The chatbot can answer questions related to a specific business, product, or domain. Unlike general chatbots (ChatGPT, etc.), a personal chatbot trained using retrieval augmented generation (RAG) can answer questions that are specific to a domain. For example, the chatbot could answer questions from your company's support technical support; or it could have specific knowledge about your business brochure, or perhaps about a specific person (such as yourself), or even about a personal hobby.

## Usage

Below is an example of calling the chatbot to answer questions from a document [climatechange.pdf](https://www.ipcc.ch/report/ar6/wg1/downloads/outreach/IPCC_AR6_WGI_SummaryForAll.pdf).

```python
vectors = initialize('climatechange.pdf')
response = chat('Who are the authors of the report?')
print(response)
```

### Output

```
The report was written by members of the Working Group I Technical Support Unit (WGI TSU) and several authors of the report. The authors are:

- Sarah Connors (WGI TSU)
- Sophie Berger (WGI TSU)
- Clotilde Péan (WGI TSU)
- Govindasamy Bala (Chapter 4 author)
- Nada Caud (WGI TSU)
...
```

## Complete Chatbot

A continuous loop allows the user to enter multiple queries for the chatbot to answer. This chatbot answers questions related to an article about [coffee](https://medium.com/illumination/i-tried-10-decaf-coffees-as-a-first-time-coffee-drinker-heres-what-i-found-a8c5fb93a40e?sk=03a1bb8109f779521d9ffec8f5f275ae).

```python
vectors = initialize('coffee.html')
while True:
    user_query = input("Enter your query (type 'quit' or 'exit' to stop): ")
    if user_query.lower() in ['quit', 'exit']:
        print("Exiting the chat. Goodbye!")
        break
    print('--------------------')
    print(f"User: \"{user_query}\"")
    response = chat(user_query)
    print("AI:", response, flush=True)
```

### Output

```
User: "Which coffee has the highest rating?"
AI: The highest-rated coffee in the review is Merit Coffee Espresso Decaf.
--------------------
User: "What was the author afraid that coffee might do to them?"
AI: The author was afraid that coffee might stain their teeth, upset their stomach, or make them jittery.
--------------------
User: "Who is the author?"
AI: The author of the article is Kory Becker.
--------------------
User: "How was the review for Folgers decaf?"
AI: The Folgers Instant Decaf coffee was ranked 8th in the list. It was described as having a bitter and dark flavor, with no impact on the stomach or caffeine effect. The coffee flakes dissolved quickly in water, and the price was noted as being a bit more expensive compared to some other options.
```

## Features

- Natural language understanding
- Context-aware responses
- Integration with external knowledge bases
- Scalable and modular architecture

## How does it work?

The chatbot works by allowing users to upload documents (text files, PDF documents, HTML pages) from which the chatbot will utilize the content for constructing its responses.

1. Each document is [stemmed](https://www.ibm.com/think/topics/stemming) and split into chunks (i.e., sentences and paragraphs).
2. The chunks are converted into a numeric vector.
3. The user enters a query for the chatbot.
4. The user's query is stemmed and converted into a numeric vector.
5. The user's query is matched agaist the database of content using a text similarity algorithm.
6. The top-N matches are included in the prompt as context, along with the user's query, and sent to an LLM.
7. The LLM uses the context to answer the question and respond to the user.

## License

MIT

## Author

Kory Becker
https://primaryobjects.com
