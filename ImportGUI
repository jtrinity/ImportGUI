import os
import wx
import ChannelPlot

class NewFrame(wx.Frame):
    def __init__(self, parent, title):
        wx.Frame.__init__(self, parent, title = title, size = (600, 300))
        self.panel = wx.Panel(self, wx.ID_ANY)
        self.CreateStatusBar()

        #entry fields

        self.pathLabel = wx.StaticText(self.panel, wx.ID_ANY, 'File:', pos = (20,20))
        self.pathField = wx.TextCtrl(self.panel, wx.ID_ANY, '', pos = (100, 20), size = (400, 20))
        self.channelLabel = wx.StaticText(self.panel, wx.ID_ANY, 'Channels:', pos = (20, 60))
        self.channelField = wx.TextCtrl(self.panel, wx.ID_ANY, '8', pos = (100, 60))
        self.dtypeLabel = wx.StaticText(self.panel, wx.ID_ANY, 'Data type:', pos = (20, 100))
        self.dtypeField = wx.TextCtrl(self.panel, wx.ID_ANY, '<d', pos = (100, 100))
        self.openLabel = wx.StaticText(self.panel, wx.ID_ANY, 'Open file:', pos = (20, 140))
        self.openField = wx.StaticText(self.panel, wx.ID_ANY, '...', pos = (100, 140))

        #buttons
        self.pathButton = wx.Button(self.panel, wx.ID_ANY, label = '...', pos = (510, 15), size = (40,20))
        self.openButton = wx.Button(self.panel, wx.ID_ANY, label = 'open', pos = (100, 180), size = (60, 20))
        self.plotButton = wx.Button(self.panel, wx.ID_ANY, label = 'plot graph', pos = (180, 180), size = (90, 20))
        self.saveButton = wx.Button(self.panel, wx.ID_ANY, label = 'save to .csv', pos = (290, 180), size = (100, 20))

        #Setting up the menu
        filemenu = wx.Menu()

        menuAbout = filemenu.Append(wx.ID_ABOUT, "&About","Information about this program")
        menuExit = filemenu.Append(wx.ID_EXIT, "E&xit", "Terminate the program")
        menuOpen = filemenu.Append(wx.ID_OPEN, "&Open", "Choose a file to open")

        #creating the menubar
        menuBar = wx.MenuBar()
        menuBar.Append(filemenu, "&File") #adding filemenu to the menubar

        self.SetMenuBar(menuBar) #adding the MenuBar to the frame  content

        #set events
            #menu binds
        self.Bind(wx.EVT_MENU, self.OnExit, menuExit)
        self.Bind(wx.EVT_MENU, self.OnAbout, menuAbout)
        self.Bind(wx.EVT_MENU, self.OnOpen, menuOpen)

            #button binds
        self.pathButton.Bind(wx.EVT_BUTTON, self.OnOpen)
        self.openButton.Bind(wx.EVT_BUTTON, self.OpenFile)
        self.plotButton.Bind(wx.EVT_BUTTON, self.Plot)
        self.saveButton.Bind(wx.EVT_BUTTON, self.OnSave)
        
        self.Centre()
        self.Show(True)

        self.dirname = ''
            
    def OnAbout(self, e):
        dlg = wx.MessageDialog(self, "A simple tool for importing and viewing interleaved binary data files.", "About:", wx.OK)
        dlg.ShowModal() #show dialog
        dlg.Destroy()

    def OnExit(self, e):
        self.Close(True) # close the frame

    #Open a file
    def OnOpen(self, e):
        self.dirname = ''
        dlg = wx.FileDialog(self, "Choose a file", self.dirname, "","*.*", wx.OPEN)
        if dlg.ShowModal() == wx.ID_OK:
            self.filename = dlg.GetFilename()
            self.dirname = dlg.GetDirectory()
            self.fullPath = os.path.join(self.dirname, self.filename)
            self.pathField.SetValue(self.fullPath)
            

        dlg.Destroy()

    def OpenFile(self, e):
        path = self.pathField.GetValue()
        workingFile.setFilename(path)
        channels = self.channelField.GetValue()
        workingFile.setTotalChannels(int(channels))
        dtype = self.dtypeField.GetValue()
        workingFile.setDataType(dtype)
        workingFile.openDataFile()
        self.openField.SetLabel(path)

    def Plot(self, e):
        workingFile.plotData()

    def OnSave(self, e):
        dlg = wx.FileDialog(self, "Save As", self.dirname,"","*.csv", wx.SAVE | wx.OVERWRITE_PROMPT)
        if dlg.ShowModal() == wx.ID_OK:
            self.filename = dlg.GetFilename()
            self.dirname = dlg.GetDirectory()
            workingFile.saveToCSV(os.path.join(self.dirname, self.filename))
        dlg.Destroy()
        
        
        


if __name__ == "__main__":   
    workingFile = ChannelPlot.ChannelPlot()

    app = wx.App(False)
    dataGUI = NewFrame(None, 'Import Data')
    app.MainLoop()
