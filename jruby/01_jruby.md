!SLIDE code
# JRuby

!SLIDE code
# Calling Java

    @@@ruby
    # This is the 'magical Java require line'.
    require 'java'

    # With the 'require' above, we can now refer to things that are part of the
    # standard Java platform via their full paths.
    frame = javax.swing.JFrame.new("Window")
    label = javax.swing.JLabel.new("Hello")

    # We can transparently call Java methods on Java objects
    frame.getContentPane.add(label)
    frame.setDefaultCloseOperation(javax.swing.JFrame::EXIT_ON_CLOSE)
    frame.pack
    frame.setVisible(true)

!SLIDE code
# Third Party Libraries

    @@@ruby
    require 'path/to/mycode.jar'

!SLIDE code
# Using java


    @@@ruby
    require 'java'
    java_import java.lang.System
    version = System.getProperties["java.runtime.version"]

    require 'java'
    Sys = java.lang.System
    version = Sys.getProperties["java.runtime.version"]


