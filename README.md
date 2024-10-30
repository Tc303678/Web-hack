```python
import http.server
import socket server
import urllib.request

PORT = 8080

class Proxy(http.server.SimpleHTTPRequestHandler):
    def do_GET(self):
        self.send_response(200)
        self.send_header('Content-type', 'text/html')
        self.end_headers()

        # Forward the request to the actual URL
        url = self.path[1:]  # Remove the leading '/'
        try:
            with urllib.request.urlopen(url) as response:
                self.wfile.write(response.read())
        except Exception as e:
            self.send_error(404, f"Error fetching URL: {e}")

httpd = socketserver.TCPServer(("", PORT), Proxy)
print(f"Serving at port {PORT}")
httpd.serve_forever()
