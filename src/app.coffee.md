
# Main

Entrypoint of emma-agent-designer

    electron = require 'electron'
    # Module to control application life.
    {app, BrowserWindow} = electron
    # Module to create native browser window.
    # Global reference
    win = null

    createWindow = ->
      win = new BrowserWindow width: 800, height: 600
      win.loadURL "file://#{__dirname}/../index.html"
      # OpenDevTools
      win.webContents.openDevTools()
      # Emitted when the window is closed
      # Dereference the window object, usually you would store windows
      # in an array if your app supports multi windows, this is the time
      # when you should delete the corresponding element.
      win.on 'closed', -> win = null

This method will be called when Electron has finished initialization and is ready
to create browser windows. Some APIs can only be used after this event occurs.

    app.on 'ready', createWindow

On macOS it's common to re-create a window in the app when the
dock icon is clicked and there are no other windows open.

    app.on 'activate', -> unless win? then createWindow()


In this file you can include the rest of your app's specific main process
code. You can also put them in separate files and require them here.