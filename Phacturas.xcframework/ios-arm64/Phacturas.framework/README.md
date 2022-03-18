#  Phacturas

### Description

Simple framework to take photos to invoices. It Rerturns and UIImage, or an Error.

### Run requirements

Minimum deployment target: iOS 10.2, iPhone, and Bitcode enable to NO.

### How to use it

Generar el framework(por default derivated data)

In order to integrate the Framework, just drop(lo generado x el derivated data) in your project the Phacturas.framework, go to your target and in the GeneralTab, go to Frameworks, Lubraries and Embedded Content amd add it. Once added, in Embed, Select Embed & Sign.

Luego en build setting(en caso de que no funcione el Consumer(Ejemplo de programación)):
Framework search Paths agregar la carpeta asi:
    /Users/lariel/Library/Developer/Xcode/DerivedData/Phacturas-gmnlyesazcuheaacfbmikzzuscpf/Build/Products/Debug-iphoneos o la carpeta dnd esté alojado el framework.
NOTA: sin el Phacturas.framework.
    

Instantiate Widget class with the init method,  passing  as delegate parameter a class that will implement the widget delegate method:

let widget = Widget.init(delegate: self)

The widget delegate method to implement is: 
func invoiceScanConfirmed(invoiceImage: InvoiceImage?, error: Error?)
Depending of the circunstances, it will return a class of Type InvoiceImage, that encapsulates and UIImage property named invoiceImage, or an Error. The error that migh arise will be given by the camera controller, more likely because of the camera permissions. If camera permissions are not granted, the widget will show an alert controller warning about it, and once you tap on OK button, it will dismiss the widget with an error result.
In order to show the widget, get the ViewController from the method getInitialViewController. This method will return a ViewController, that you´ll have to present from your viewController.

It is possibe to customize the text appearing in the widget, through the following widget properties:
acceptButtonText-> Customize the current Accept button text.
takeAgainButtonText-> Customize the current Take Again button text.
captureButtonText-> Customize the current Capture Again button text.
descriptionBeforeCapture-> Customize the current Title text.
descriptionAfterCapture-> Cuztomize the current Title text.
alertTitleDescription-> Customize the current alert title text.
alertMessageDescription-> Customize the current alert message text.

Tipical Instantiation example:
In your ViewController:

@IBAction func showWidget(_ sender: Any) {
    let widget = Widget.init(delegate: self)
    let controller = widget.getInitialViewController()
    controller?.modalPresentationStyle = .fullScreen
    self.present(controller!, animated: true, completion: nil)
}

Example of how to consume the delegate:

extension ViewController: WidgetResultDelegate {
    func invoiceScanConfirmed(invoiceImage: InvoiceImage?, error: Error?) {
        guard let invoice = invoiceImage else { return }
    }
}

### Change .Framework output location.

Go to File -> Project Settings.

Click the Advanced button under Derived Data Location. Under build location select custom and choose your output directory. This will change the variable $(BUILD_DIR) to whatever you set in that field.




