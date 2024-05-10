# Server.js
Simple server using core nodes

const http = require('http');
const os = require('os');

const PORT = 3000;

const server = http.createServer((req, res) => {
  // Enable CORS
  res.setHeader('Access-Control-Allow-Origin', '*');
  res.setHeader('Access-Control-Allow-Headers', 'Origin, X-Requested-With, Content-Type, Accept');
  
  // Simulate some asynchronous operation with a random delay
  const delay = Math.floor(Math.random() * 3000) + 1000; // Random delay between 1 to 4 seconds
  setTimeout(() => {
    if (req.method === 'GET' && req.url === '/info') {
      const info = {
        cpu: os.cpus(),
        os: {
          arch: os.arch(),
          platform: os.platform(),
          release: os.release(),
          totalMemory: os.totalmem(),
          freeMemory: os.freemem(),
        },
      };
      res.writeHead(200, { 'Content-Type': 'application/json' });
      res.end(JSON.stringify(info));
    } else {
      res.writeHead(404, { 'Content-Type': 'text/plain' });
      res.end('Not Found');
    }
  }, delay);
});

server.listen(PORT, () => {
  console.log(`Server running at http://localhost:${PORT}`);
});
