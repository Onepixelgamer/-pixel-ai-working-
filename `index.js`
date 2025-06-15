module.exports = (req, res) => {
  // Set CORS headers
  res.setHeader('Access-Control-Allow-Origin', '*')
  res.setHeader('Access-Control-Allow-Methods', 'GET, POST, OPTIONS')
  res.setHeader('Access-Control-Allow-Headers', 'Content-Type')
  
  // Handle preflight
  if (req.method === 'OPTIONS') {
    res.status(200).end()
    return
  }

  const { url, method } = req

  // Root endpoint
  if (url === '/' && method === 'GET') {
    res.status(200).json({
      message: '🤖 PIXEL AI Server is running!',
      status: 'healthy',
      timestamp: new Date().toISOString()
    })
    return
  }

  // Health endpoint
  if (url === '/health' && method === 'GET') {
    res.status(200).json({
      status: 'healthy',
      message: 'PIXEL AI Server is working!',
      timestamp: new Date().toISOString()
    })
    return
  }

  // Build endpoint
  if (url === '/api/build/request' && method === 'POST') {
    let body = ''
    req.on('data', chunk => body += chunk)
    req.on('end', () => {
      try {
        const data = JSON.parse(body)
        res.status(200).json({
          success: true,
          buildId: `BUILD_${Date.now()}`,
          message: `Building: ${data.description || 'something awesome'}`,
          instructions: ['Create foundation', 'Build structure', 'Add details']
        })
      } catch (e) {
        res.status(400).json({ error: 'Invalid JSON' })
      }
    })
    return
  }

  // 404 for everything else
  res.status(404).json({
    error: 'Not found',
    url: url,
    method: method
  })
}
