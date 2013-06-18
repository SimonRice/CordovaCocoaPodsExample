platform :ios, "5.0"
CORDOVA_VERSION = "2.8.0"

pod "Cordova", CORDOVA_VERSION

post_install do | installer |
  # Download Cordova.js for iOS
  
  require 'net/http'
  require 'fileutils'
  require 'openssl'
  
  FileUtils.mkdir_p("www") unless File.directory?("www")
  f = open("www/cordova.js", "w+") 
  
  uri = URI.parse("https://raw.github.com/apache/cordova-ios/#{CORDOVA_VERSION}/CordovaLib/cordova.js")
  http = Net::HTTP.new(uri.host, uri.port)
  http.use_ssl = true
  http.verify_mode = OpenSSL::SSL::VERIFY_NONE
  
  response = http.request(Net::HTTP::Get.new(uri.request_uri))
  begin
    f.write(response.body)
  ensure
    f.close()
  end
end
