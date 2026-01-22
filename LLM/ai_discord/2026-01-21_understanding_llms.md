<h1>Understanding Large Language Models (LLMs) </h1>


<h3>What is LLMs </h3>
Large Language Models (LLMs) is a type of AI that is designed to understand and generate humanlike text based on the input or the instruction that it receives.
There are two ways to access LLMs. One is `Open Source LLMs` and `Closed Source LLMs`. Closed Source LLMs are proprietary models that are developed by organizations like 
OpenAI, Anthropic, and Cohere. Closed Source are own by organizations and they have the authority to modify and distribute the code and you have to pay in order to use the models.
You can use GPT-4o by using CHATGPT application for free but if you want to build something on top of it, you'll have to access it through APIs.
Open Source like Llama from Meta. Since its open source, anyone can set up and run their own models on their local machine or on a cloud.

<h3>What is API and RESTful API </h3>

API (Application Programming Interface) is a set of definitions and protocols for building and integrating application software. 
Sometimes referred as a contract between an infomation provide and an infromation user-establishing the content required from the consumer
(the call) and the content required by the producer (the repsonse). If you weant to interact with a computer or system to retrieve information
or perform a function, an API help you communicate what you want to that system so it can understand and fulfill the request. 
For example, the API design for a weather service could specify that the user supply a zip code and that the producer reply with a 2-part answer,
the first being the high temperature, and the second being the low. 

REST is a set of architectural constraints, not a protocol or a standard. It is a set of rules that has been the common standard for building web API. 
 ```console
 1. Uniform Interface
 2. Client-Server
 3. Stateless
 4. Cacheable
 5. Layered System
 6. Code on Demand (optional)
 ```
A API that follows the REST standard is called a RESTful API. Google maps is a RESTful API. A RESTFUL API organize resource into a set of unqiue URI (unifrom resource identifiers)
The URIs differentiate different type of resources on a server. The resources should be group by nouns and not verb. An API to get all products should be /products and not /getAllProduct.
A client interacts with a resource by making a request to the endpoint for the resource over HTTP. 

<h3>Building with LLMs using Ollama </h3>
For close source model like OpenAI, they offer APIs we can use. However for open source model, we can use Ollama. Ollama is a tool that provides a library of pre-build models and we
can pull the existing models. It also offers a REST API (REpresentation State Transfer Application Programming) for more adcance use cases.
