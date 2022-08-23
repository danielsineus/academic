---
# An instance of the Contact widget.
widget: contact

# This file represents a page section.
headless: true

# Order that this section appears on the page.
weight: 130

title: Contact
subtitle:

content:
  # Automatically link email and phone or display as text?
  autolink: true

  # Email form provider
  form:
    provider: netlify
    formspree:
      id:
    netlify:
      # Enable CAPTCHA challenge to reduce spam?
      captcha: false

  # Contact details (edit or remove options as required)
  email: dsineus2020@fau.edu
  #phone: 888 888 88 88
  address:
    #street: 1875 Calida Dr
    city: West Palm beach
    region: FL
    postcode: '33411'
   # country: United States
    #country_code: US
  #coordinates:
    latitude: '37.4275'
    longitude: '-122.1697'
  #directions: Enter Building 1 and take the stairs to Office 200 on Floor 2
  office_hours:
    - 'Friday 5:00 to 8:00 Eastern Time'
    - 'Saturday 09:00 to 12:00 Eastern Time'
  appointment_url: 'https://calendly.com'
  contact_links:
    - icon: twitter
      icon_pack: fab
      name: DM Me
      link: 'https://twitter.com/DanielSineus'
    - icon: video
      icon_pack: fas
      name: Zoom Me
      link: 'https://zoom.com'

design:
  columns: '2'
---
