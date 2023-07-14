# PDFKit-SwiftUI
A button to open PDF.
# The first part
![IMG_0308](https://github.com/S-way520/PDFKit-SwiftUI/assets/95877651/acb730ef-20be-4ea5-9aa9-9ae982a8827a)
# The second part
Code file 1
```swift
import SwiftUI
@main
struct MyApp: App {
    var body: some Scene {
        WindowGroup {
            ContentView()
        }
    }
}
struct ContentView: View {
    @State var Show = false
    var body: some View {
        MPDF(Show: Show, PDFname: "RealityKit", PDFnameD: "RealityKit")
    }
}
```
Code file 2
```swift
import SwiftUI
import PDFKit
struct PDFKitView: View {
    var url: URL
    var body: some View {
        MapPDFView1(url)
    }
}
struct MapPDFView1: UIViewRepresentable {
    let url: URL
    init(_ url: URL) {
        self.url = url
    }
    func makeUIView(context: UIViewRepresentableContext<MapPDFView1>) -> MapPDFView1.UIViewType {
        let pdfView = PDFView()
        //pdfView.backgroundColor = .blue
        pdfView.document = PDFDocument(url: self.url)
        pdfView.autoScales = true
        return pdfView
    }
    func updateUIView(_ uiView: UIView, context: UIViewRepresentableContext<MapPDFView1>) {
    }
}
struct MapPDFView_Previews: PreviewProvider {
    static var previews: some View {
        PDFKitView(url: Bundle.main.url(forResource: "RealityKit", withExtension: "pdf")!
        );}
}
//MARK: A way to show the PDF book
struct MPDF: View {
    @Environment(\.colorScheme) var colorScheme
    func simpleSuccess() {UINotificationFeedbackGenerator().notificationOccurred(.success)}
    @State var Show = false
    var PDFname: String
    var PDFnameD: String
    var body: some View {
        Button(action: { Show.toggle() }){
            Image(systemName: "book.closed")
                .foregroundColor(.orange)
                .font(.title2)
        }
        .sheet(isPresented: $Show){
            ZStack {
                PDFKitView(url: Bundle.main.url(forResource: (colorScheme == .light ?  PDFnameD : PDFname), withExtension: "pdf")!)
                VStack{
                    HStack{
                        Spacer()
                        Button(action: {self.Show.toggle(); simpleSuccess()}) {
                            Image(systemName: "multiply.circle")
                                .font(.title)
                                .padding()
                        }
                    }
                    Spacer()
                }
            }
        }
    }
}
```
