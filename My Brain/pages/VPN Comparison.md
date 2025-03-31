tags:: #VPN #Shadowrocket #Mullvad #apolloapp 
parent:: #VPN
prompt:: [[Apollo Prompt]] 
LLM:: [[Gemini]] Flash 2.0
description:: VPN Comparison between Express VPN, Shadowrocket and Wireguard

- User: What is the difference between Express VPN and [[Shadowrocket]] and Wireguard VPNs?
  id:: 67eade5b-c10c-4aa8-a36e-c73651591c45
	- Assistant: **ExpressVPN** is a premium VPN service offering its own protocols (like Lightway) focused on privacy and speed. While they initially found **WireGuard** promising, they noted its anonymity challenges in 2019 ([expressvpn.com](https://www.expressvpn.com)). Since then, services integrating WireGuard (or modified versions) highlight its open-source efficiency and modern cryptography for speed and security ([allaboutcookies.org](https://allaboutcookies.org)).
	- **Shadowrocket** is an iOS proxy client app, not a VPN service itself—it lets you configure VPN protocols (including WireGuard) with third-party servers.
	  id:: 67eade5b-ec91-467a-be4b-8e80fa4f58c8
	- **Key differences**:
		- *ExpressVPN*: Full-service provider with proprietary apps and protocols.
		- *Shadowrocket*: A tool to set up VPNs but not a standalone VPN.  
		  id:: 67ead7dc-775a-4018-8eb5-97abe37457fa
		  collapsed:: true
		- *WireGuard*: A lightweight protocol (used by some VPNs), prioritizing speed and simplicity over built-in anonymity features.  
		  
		  For WireGuard-based VPNs in 2025, see options tested here: [vpnmentor.com](https://www.vpnmentor.com).
- User: What is the best all round VPN without logs and lots of locations (like Albania) for privacy?
	- Assistant: For a **no-logs VPN** with diverse server options (including Albania), prioritize **[[Mullvad VPN]]** ([mullvad.net](https://mullvad.net/en)):
		- **Zero personal data required** (not even an email).
		- Servers in Albania and 45+ countries.
		- Open-source apps + WireGuard support for speed/security.  
		  
		  **Alternatives**:
		- **Private Internet Access** ([privateinternetaccess.com](https://www.privateinternetaccess.com)): Audited no-logs policy tested twice in court, 90+ countries (Albania confirmed).
		- **AirVPN** ([airvpn.org](https://airvpn.org)): Anonymous sign-ups, strong focus on transparency.  
		  
		  All three avoid invasive tracking and allow Albanian IPs. Mullvad’s refusal to collect *any* user data gives it a slight edge for privacy purists.
- User: Additional criteria is the availability of an Apple TV app
	- Assistant: Okay, considering your requirement for an Apple TV app in addition to a no-logs policy and Albanian servers, here's the updated recommendation:
	  
	  **ExpressVPN**([expressvpn.com](https://www.expressvpn.com)) is a great choice:
	- No-logs policy verified by audits.
	- Servers available in Albania.
	- Dedicated app for Apple TV. Offers fast speeds with their Lightway protocol.
	  
	  **NordVPN** ([nordvpn.com](https://nordvpn.com)) is another strong option:
	- Audited no-logs policy.
	- Server locations include Albania.
	- Also has a native app for Apple TV. Uses Nordlynx (WireGuard-based).
	  
	  Both meet all your criteria. The choice between them is often down to personal preference on features and pricing.
- User: What are the main differences between them?
	- Assistant: Here's a quick comparison of ExpressVPN and NordVPN, based on the most common differences:
	  
	  *   **Speed:** ExpressVPN's Lightway protocol is known for very fast speeds and great performance. NordVPN's NordLynx(WireGuard) is very fast too. Both are top-tier.
	  *   **Server locations:** NordVPN has a larger network with more servers overall. ExpressVPN maintains a solid global spread, including Albania for both.
	  *   **User interface:** Both have user-friendly apps, but the specific design may influence your choice based on preference.
	  *   **Price:** Both are premium VPNs hence they are similarly priced. Consider discounts & promotional offers.
	  *   **Features:** NordVPN has features like Threat Protection to block ads and trackers, and Meshnet for directly connecting devices. ExpressVPN provides MediaStreamer (Smart DNS).
	  
	  In short, while both are excellent, ExpressVPN might be preferred if speed is the *absolute* priority, or if you *absolutely* want MediaStreamer. NordVPN shines with broader feature set, and a larger server network.
- User: Can you display the results in table format?
	- Assistant: Okay, here's a table summarizing the key differences between ExpressVPN and NordVPN:
	  
	  | Feature          | ExpressVPN                                  | NordVPN                                      |
	  |-------------------|---------------------------------------------|----------------------------------------------|
	  | **Speed**         | Very Fast (Lightway protocol)               | Very Fast (NordLynx/WireGuard)              |
	  | **Server Network**| Solid Global Coverage, including Albania   | Larger Network, including Albania           |
	  | **User Interface**| User-Friendly (Preference Dependent)       | User-Friendly (Preference Dependent)          |
	  | **Price**         | Premium Pricing (Check for deals)        | Premium Pricing (Check for Deals)            |
	  | **Extra Features**| MediaStreamer (Smart DNS)                   | Threat Protection, Meshnet                   |
	  | **Apple TV App**  | Yes                                         | Yes                                          |
	  | **No-Logs Policy**| Audited                                     | Audited                                      |
- User: What are the latest promotions for Express VPN?
	- Assistant: Okay, let's check for the latest ExpressVPN promotions. Based on my current search results:
	  
	  *   **MKBHD Offer:** They have an offer promoted by Marques Brownlee (MKBHD) for **15 months** of ExpressVPN [expressvpn.com](https://www.expressvpn.com/mkbhd-vpn?srsltid=AfmBOooW5KTJDSOnzbzPCWZ_XrLWUR2sSY_EG63Pb9LTJv8A0AcfEpeR).
	  
	  *   **General Deals:** ExpressVPN often has deals, offering extra months free with subscriptions [expressvpn.com](https://www.expressvpn.com/coupons?srsltid=AfmBOor_5xYajUYYr49YaXnz10rWSQMrteMAR_AcyPFG6kSYYst6Swp2).
	  
	  *   **Seasonal Sales:** Keep an eye out for seasonal sales like Black Friday, Cyber Monday etc [techradar.com](https://www.techradar.com/coupons/express-vpn).
	  
	  It's always a good idea to visit the ExpressVPN website directly to confirm the most up-to-date offers.
- User: Does express vpn work in China?
	- Assistant: The situation with ExpressVPN in China is a bit complicated. Here's what the search results suggest:
	  
	  *   **It can work, but it's not guaranteed:** ExpressVPN is one of the few VPNs that *can* work in China, but it's not a sure thing [www.vpncompare.co.uk](https://www.vpncompare.co.uk/does-expressvpn-work-china).
	  *   **China blocks VPNs:** The Chinese government heavily regulates and blocks VPNs that don't have official licenses [www.comparitech.com](https://www.comparitech.com/blog/vpn-privacy/expressvpn-china/).
	  *   **Mirror Site:** ExpressVPN uses mirror sites [www.vpnmentor.com](https://www.vpnmentor.com/blog/expressvpn-works-in-china-but-only-if-you-do-this/)
	  *   **Configuration:** You might need to configure the app to maximize your chances of getting it working [www.safetydetectives.com](https://www.safetydetectives.com/blog/does-expressvpn-work-in-china/).
	  *   **Not Always Reliable:** Due to China's ongoing efforts to block VPNs, ExpressVPN can be hard to use there [www.cloudwards.net](https://www.cloudwards.net/expressvpn-china/).
	  
	  So, while ExpressVPN *can* work, be prepared for potential difficulties and the need for configuration.