const { spawn } = require('child_process')

function execCmd(cmd) {
  return new Promise((resolve, reject) => {
    const child = spawn(cmd, { shell: true, stdio: 'inherit' })
    child.on('close', code => {
      if (code !== 0) {
        reject(code)
      } else {
        resolve()
      }
    })
    child.on('error', reject)
  })
}

namespace('server', () => {
  desc('Starting server')
  task('start', async function () {
    await execCmd('./npm-scripts/start-server.sh')
  })
})

namespace('client', () => {
  desc('Starting client')
  task('start', async function () {
    setTimeout(async () => {
      await execCmd('./npm-scripts/start-client.sh')
    }, 3000)
  })
})

desc('Start client and server')
task('run', ['client:start', 'server:start'], {
  concurrency: 2,
})
