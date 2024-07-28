# HTTPie CLI Cheat Sheet

## Basic Usage

| Syntax | Description |
|--------|-------------|
| `http [flags] [METHOD] URL [ITEM [ITEM]]` | General syntax for HTTPie commands |

## Common Commands and Options

| Category | Command/Option | Description | Example |
|----------|----------------|-------------|---------|
| **HTTP Methods** | GET | Default method | `http example.com` |
| | POST | Send data | `http POST example.com` |
| | PUT | Update resource | `http PUT example.com` |
| | DELETE | Delete resource | `http DELETE example.com` |
| **Request Headers** | Custom header | Add a single header | `http example.com X-MyHeader:123` |
| | Multiple headers | Add multiple headers | `http example.com X-Header1:123 X-Header2:456` |
| **Request Data** | JSON data | Send JSON data | `http POST example.com name=John age:=30` |
| | Form data | Send form data | `http -f POST example.com name="John Doe" age=30` |
| | File contents | Send file contents | `http example.com < file.json` |
| **Authentication** | Basic auth | Use basic authentication | `http -a username:password example.com` |
| | Bearer token | Use bearer token | `http example.com "Authorization:Bearer token"` |
| **Output Options** | Verbose output | Show detailed info | `http -v example.com` |
| | Headers only | Show only headers | `http -h example.com` |
| | Body only | Show only body | `http -b example.com` |
| | Save output | Save response to file | `http example.com > response.json` |
| **Session** | Start session | Begin a new session | `http --session=mysession example.com` |
| | Use session | Use existing session | `http --session=mysession example.com` |

### Examples of Typical Use Cases

| Use Case | Command |
|----------|---------|
| Simple GET request | `http https://api.github.com/users/octocat` |
| POST with JSON data | `http POST https://jsonplaceholder.typicode.com/posts title="My Post" body="This is the content" userId:=1` |
| PUT to update resource | `http PUT https://jsonplaceholder.typicode.com/posts/1 id:=1 title="Updated Title" body="Updated content" userId:=1` |
| DELETE request | `http DELETE https://jsonplaceholder.typicode.com/posts/1` |
| GET with query parameters | `http https://api.github.com/search/repositories q==httpie language==python` |
| POST with form data | `http -f POST https://httpbin.org/post name="John Doe" age:=30 newsletter:=true` |
| GET with custom headers | `http https://api.example.com/data "Authorization:Bearer mytoken" "Accept:application/json"` |

## Handling Complex Data Structures

### Objects, Arrays, and Arrays of Objects

| Data Structure | Command/Syntax | Description |
|----------------|----------------|-------------|
| **Array** | `http POST example.com fruits:='["apple", "banana", "cherry"]'` | Send a JSON array |
| **Object** | `http POST example.com name=John age:=30 "address[street]"="123 Main St" "address[city]"="Anytown"` | Send a JSON object |
| **Array of Objects** | `http POST example.com users:='[{"name": "John", "age": 30}, {"name": "Jane", "age": 28}]'` | Send an array of JSON objects |

### Examples of Complex Data Structures

| Use Case | Command |
|----------|---------|
| POST request with nested object | `http POST https://api.example.com/users name=John age:=30 "address[street]"="123 Main St" "address[city]"="Anytown" "address[zip]"="12345"` |
| POST request with array | `http POST https://api.example.com/todos tasks:='["Buy groceries", "Clean house", "Walk dog"]'` |
| POST request with array of objects | `http POST https://api.example.com/orders items:='[{"product": "Widget", "quantity": 2, "price": 9.99}, {"product": "Gadget", "quantity": 1, "price": 24.99}]'` |
| PUT request updating nested fields | `http PUT https://api.example.com/users/123 "preferences[theme]"=dark "preferences[notifications][email]"=true "preferences[notifications][sms]"=false` |

## Tips for Working with Complex Data

1. Use single quotes to wrap JSON arrays and objects to avoid shell interpretation.
2. For deeply nested structures, consider using a JSON file: `http POST example.com < data.json`
3. Use `:=` for numbers and booleans to ensure they're sent as JSON, not strings.
4. For very complex structures, you can use inline JSON: `http POST example.com data:='{"key": {"nested": [1, 2, 3]}}'`

Remember that when sending complex data structures, it's crucial to format them correctly to ensure they're interpreted as valid JSON by the server.

## Tips for Advanced Usage

| Tip | Command/Option | Description |
|-----|----------------|-------------|
| 1 | `--print=HBhb` | See both request and response headers and bodies |
| 2 | `--verify=no` | Skip SSL certificate verification (use with caution) |
| 3 | `--timeout=30` | Set a custom timeout for requests |
| 4 | `--follow` | Automatically follow redirects |
| 5 | `--download` | Download files instead of displaying them |
| 6 | `--proxy=http:http://proxy.example.com:8080` | Use a proxy server |
| 7 | `--style=autumn` | Change the color scheme of the output |
| 8 | `--pretty=all` or `--pretty=colors` | Format and colorize the output |
| 9 | `--offline` | Build a request without sending it |
| 10 | `--debug` | See the complete HTTP exchange for debugging |

Remember to check `http --help` or visit the official HTTPie documentation for more detailed information and the most up-to-date options.
