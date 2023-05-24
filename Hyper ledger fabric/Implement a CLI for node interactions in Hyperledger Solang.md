### Description 

[Hyperledger Solang](https://github.com/hyperledger/solang) is a Solidity compiler written in Rust. It currently targets [Substrate](https://github.com/paritytech/substrate) [contracts pallet](https://github.com/paritytech/substrate/tree/master/frame/contracts) (Polkadot) and [Solana](https://github.com/solana-labs/solana) smart contract runtimes. After successful compilation, users need to upload the compiled contract artifacts to a blockchain node, so it can be interacted with. At the time of writing, this needs to be done manually via third-party web front-ends. Which results in an inefficient and tiring process during iterative contract development.  

The goal of this mentorship is to implement a Command Line Interface (CLI) for Solang that can be used for node interactions instead. This includes uploading and deploying contracts on-chain as well as submitting transactions to contracts.

- #### Additional Information

	We expect the Student to perform the following tasks:
		
	-   Gather requirements and outline a generic interface that will be usable for both supported targets (Substrate and Solana).
	-   Implement the CLI as a sub-commands for Solang.  
		-   For the Substrate target;  [cargo-contract](https://crates.io/crates/cargo-contract/) already provides a CLI for node interactions (Substrate target), however it does not yet support Solidity contracts.
		    -   For the Solana target
		-   Describe the CLI in Solang's [documentation](https://solang.readthedocs.io/en/latest/).

- #### Learning Objectives

	- By working on open source code bases, Students will learn and experience practical aspects of software engineering such as:

		-   Designing re-usable interfaces
			-   Analyzing and understanding code bases of reasonable sizes
				-   Refactoring existing components and implementing new features in Rust
				-   Contributing maintainable code to open source projects
				-   Getting proficient in working with tools like git
			Additionally, students will learn about smart contracts, Substrate and Solana in general.

- #### Expected Outcome

	-   Solang provides a working and documented CLI for node interactions with Substrate and Solana. Options for sub-commands (like RPC end-point, account to use, dry-run flag, gas limits, verbosity and other specific options) must be configurable by the user.  
				-   A sub-command for uploading contracts.
			    -   A sub-command for instantiating contracts.
			    -   A sub-command for calling contract functions. This command must correctly encode transaction input, display and show the calls output and debug output as well as emitted events.
			    -   A sub-command for listening to emitted events.
			-   The student should factor the relevant parts of cargo-contract out into a dedicated library (crate) to make it usable in Solang.
			-   Developed source code is of adequate quality, merged in the projects upstream repositories and have undergone common Pull Request processes.
- #### Relation to Hyperledger 

	The Solang Solidity compiler is a Hyperledger project.

- #### Mentee Skills

	We accept students from all educational levels with a background in computer science or a related field. We expect students to either be already familiar with Rust programming language basics such as [Understanding Ownership](https://doc.rust-lang.org/stable/book/ch04-00-understanding-ownership.html) and [Generics](https://doc.rust-lang.org/stable/book/ch10-00-generics.html), OR to demonstrate their ability and willingness to learn them in a timely manner.

	Bringing any of the following skills is of advantage but not strictly required:

	-   Knowledge of blockchain technology and smart contracts
		-   Prior contributions to open source projects
		-   If no prior Rust experience, good knowledge of C++ is of advantage
		-   Basic knowledge of git

- #### Future plans

	This feature is an important building block for integrations with common Solidity development tools like truffle or hardhat. Additionally, it will greatly improve the user experience of Solang. For Solidity developers, we expect it to become the default way of interacting with our target blockchain nodes.
-<br><br>
- ## ChatGPT
	- Based on this job description, wthat is the biggest challenge someone in this position would face day to day ?
	- ### Description 

[Hyperledger Solang](https://github.com/hyperledger/solang) is a Solidity compiler written in Rust. It currently targets [Substrate](https://github.com/paritytech/substrate) [contracts pallet](https://github.com/paritytech/substrate/tree/master/frame/contracts) (Polkadot) and [Solana](https://github.com/solana-labs/solana) smart contract runtimes. After successful compilation, users need to upload the compiled contract artifacts to a blockchain node, so it can be interacted with. At the time of writing, this needs to be done manually via third-party web front-ends. Which results in an inefficient and tiring process during iterative contract development.  

The goal of this mentorship is to implement a Command Line Interface (CLI) for Solang that can be used for node interactions instead. This includes uploading and deploying contracts on-chain as well as submitting transactions to contracts.

- #### Additional Information

	We expect the Student to perform the following tasks:
		
	-   Gather requirements and outline a generic interface that will be usable for both supported targets (Substrate and Solana).
	-   Implement the CLI as a sub-commands for Solang.  
		-   For the Substrate target;  [cargo-contract](https://crates.io/crates/cargo-contract/) already provides a CLI for node interactions (Substrate target), however it does not yet support Solidity contracts.
		    -   For the Solana target
		-   Describe the CLI in Solang's [documentation](https://solang.readthedocs.io/en/latest/).

- #### Learning Objectives

	- By working on open source code bases, Students will learn and experience practical aspects of software engineering such as:

		-   Designing re-usable interfaces
			-   Analyzing and understanding code bases of reasonable sizes
				-   Refactoring existing components and implementing new features in Rust
				-   Contributing maintainable code to open source projects
				-   Getting proficient in working with tools like git
			Additionally, students will learn about smart contracts, Substrate and Solana in general.

- #### Expected Outcome

	-   Solang provides a working and documented CLI for node interactions with Substrate and Solana. Options for sub-commands (like RPC end-point, account to use, dry-run flag, gas limits, verbosity and other specific options) must be configurable by the user.  
				-   A sub-command for uploading contracts.
			    -   A sub-command for instantiating contracts.
			    -   A sub-command for calling contract functions. This command must correctly encode transaction input, display and show the calls output and debug output as well as emitted events.
			    -   A sub-command for listening to emitted events.
			-   The student should factor the relevant parts of cargo-contract out into a dedicated library (crate) to make it usable in Solang.
			-   Developed source code is of adequate quality, merged in the projects upstream repositories and have undergone common Pull Request processes.
- #### Relation to Hyperledger 

	The Solang Solidity compiler is a Hyperledger project.
<br><br>

################################################
	  - How did you find out about our mentorship progra	
	  - Why are you interested in this program? 
	   - What experience and knowledge/skills do you have that are applicable to this program? 
	   - What do you hope to get out of this mentorship experience?
################################################
<br>
- ## ANS
	- The biggest challenge someone in this position would face day to day is likely to be designing and implementing a **generic interface that works seamlessly with both supported targets (Substrate and Solana)**. This includes understanding the requirements of both **platforms and ensuring that the CLI supports all necessary functionalities and options**. Additionally, the student would need to ensure that the **CLI is well documented and easy to use for developers who are not familiar with Solang**. Finally, they would need to f**actor the relevant parts of cargo-contract out into a dedicated library (crate) to make it usable in Solang, which could require a deep understanding of the existing codebase and extensive refactoring.**
- <br><br>
- ## Next Prompt
- You are currently a student who is exploring blockchian and you'r applying for this mentee role at Implement a CLI for node interactions in Hyperledger Solang Mentorship
- Write an attension grabbing hook for your cover letter that highlights your experience and qualifications in way that empathize and can successfully take on the challenges of the mentee role
- Consider incorporating specific example of how you've tackled these challenges in your past your based on your resume , and explore creative ways to express your enthusiasm for the opportunity. Keep your hook wwithin 100 words
- Deepjyoti Sarmah
deepjyotisarmah37@gmail.com
(+91) 6003349334
deepjyoti-sarmah-539b96202
Assam, India
Webiste
Deepjyo79836591
Deepjyoti-Sarmah
SKILLS
Programming Languages :
Solidity, JavaScript, Golang, Java, Python, C++
Tools and Technologies :
Linux, Docker, Bash Scripting Git/Github, Blockchain, Ethereum, Solana, Hardhat, Chai-testing, ReactJS, NodeJS,
ExpressJS, MongoDB/SQL, ERC20, ERC721, GoFiber, GorillaMux
PROJECTS
Creator's Fund
Website for decentralized creator funding
By connecting their wallet to the website, users can donate cryptocurrency to their
creators.
Solidity (back-end) and ReactJS and TailwindCSS (front-end) were used in its
development . Hardhat and Chai were used to test and deploy02/2023
File Storage Dapp
A decentralized file storage system
Users can save and browse their files using the decentralization file storage system built
into the web3 area.
ReactJS and TailwindCSS (front-end). Smart contracts development using Solidity and
Hardhat . Web3.stoage for storing files on IPFS, and Rainbowkit for connecting to
wallet.04/2023
Gassless AI NFTs
NFT minting dapp powered by AI
Accepts instructions from users, use stable diffusion to create art, and then distributes
this created art for free on the blockchain.
(Front-end) ReactJS and TailwindCSS. Hugging Face, a stable diffusion model for
generating art. NFTport API, for the gas less NFT creation on the blockchain.04/2023
Solana Airdrop
A website app that uses an address in a wallet to airdrop solana
A website that delivers Solana to a specific account after receiving the user's wallet
address and the amount to airdrop
Tailwind-CSS with ReactJS (front-end). Connection and transaction are handled by
Solana/Web3.js in Solana-Devnet.04/2023
•
•
•
•
•
•
•
•
EXPERIENCES
Turban-Onn
Smart India Hackathon - Grand Finalist, Software Edition
An application that displays turban filters covering a person's face in real time using
Augmented Reality
Developed an augmented reality system utilising ARCore that allowed for the real-time
application of turban filters and facial detection.06/2022 – 08/2022
Virtual Tech Notes
Community-maintained repositories for Virtual-Tech-School
An open source community that maintains notes for various technology and boot-camps
Actively enhanced and contributed to the Linux-masterclass and Git-masterclass
sections of the documentation, which led to a 10% increase in the number of forks2022 – present
•
•
•
•
EDUCATION
Computer Science And Engineering
Assam University, Silchar
CGPA: 7.80 (Till 3rd Year)

- #### ANS
- "I am thrilled to apply for the mentee role at Implementing a CLI for Node Interactions in Hyperledger Solang Mentorship. As a blockchain enthusiast and a student exploring the industry, I am excited to take on the challenges of this role. My experience in developing decentralized applications, proficiency in various programming languages, and familiarity with tools and technologies such as Solidity, Docker, and Git/Github make me a perfect fit for this opportunity. I have successfully tackled similar challenges in my past projects, such as building a decentralized file storage system using ReactJS, Solidity, and Hardhat. I am eager to bring my skills, creativity, and enthusiasm to this project and learn from experienced mentors in the field."
- <br><br>
- ### Next prompt
- you are writing a cover letter applying for the mentee role at Implement a CLI for node interactions in Hyperledger Solang. Here's is what you have so far:
-  "I am thrilled to apply for the mentee role at Implementing a CLI for Node Interactions in Hyperledger Solang Mentorship. As a blockchain enthusiast and a student exploring the industry, I am excited to take on the challenges of this role. My experience in developing decentralized applications, proficiency in various programming languages, and familiarity with tools and technologies such as Solidity, Docker, and Git/Github make me a perfect fit for this opportunity. I have successfully tackled similar challenges in my past projects, such as building a decentralized file storage system using ReactJS, Solidity, and Hardhat. I am eager to bring my skills, creativity, and enthusiasm to this project and learn from experienced mentors in the field."
- finish writing the cover letter bases on your resume and keep it within 250 words. Also include this points as asked by the cover letter 
-  How did you find out about our mentorship program	
- Why are you interested in this program? 
- What experience and knowledge/skills do you have that are applicable to this program? 
- What do you hope to get out of this mentorship experience?
- tell that you found out about the program which searching to blockchain realword project ideas
- 
-  Deepjyoti Sarmah
deepjyotisarmah37@gmail.com
(+91) 6003349334
deepjyoti-sarmah-539b96202
Assam, India
Webiste
Deepjyo79836591
Deepjyoti-Sarmah
SKILLS
Programming Languages :
Solidity, JavaScript, Golang, Java, Python, C++
Tools and Technologies :
Linux, Docker, Bash Scripting Git/Github, Blockchain, Ethereum, Solana, Hardhat, Chai-testing, ReactJS, NodeJS,
ExpressJS, MongoDB/SQL, ERC20, ERC721, GoFiber, GorillaMux
PROJECTS
Creator's Fund
Website for decentralized creator funding
By connecting their wallet to the website, users can donate cryptocurrency to their
creators.
Solidity (back-end) and ReactJS and TailwindCSS (front-end) were used in its
development . Hardhat and Chai were used to test and deploy02/2023
File Storage Dapp
A decentralized file storage system
Users can save and browse their files using the decentralization file storage system built
into the web3 area.
ReactJS and TailwindCSS (front-end). Smart contracts development using Solidity and
Hardhat . Web3.stoage for storing files on IPFS, and Rainbowkit for connecting to
wallet.04/2023
Gassless AI NFTs
NFT minting dapp powered by AI
Accepts instructions from users, use stable diffusion to create art, and then distributes
this created art for free on the blockchain.
(Front-end) ReactJS and TailwindCSS. Hugging Face, a stable diffusion model for
generating art. NFTport API, for the gas less NFT creation on the blockchain.04/2023
Solana Airdrop
A website app that uses an address in a wallet to airdrop solana
A website that delivers Solana to a specific account after receiving the user's wallet
address and the amount to airdrop
Tailwind-CSS with ReactJS (front-end). Connection and transaction are handled by
Solana/Web3.js in Solana-Devnet.04/2023
•
•
•
•
•
•
•
•
EXPERIENCES
Turban-Onn
Smart India Hackathon - Grand Finalist, Software Edition
An application that displays turban filters covering a person's face in real time using
Augmented Reality
Developed an augmented reality system utilising ARCore that allowed for the real-time
application of turban filters and facial detection.06/2022 – 08/2022
Virtual Tech Notes
Community-maintained repositories for Virtual-Tech-School
An open source community that maintains notes for various technology and boot-camps
Actively enhanced and contributed to the Linux-masterclass and Git-masterclass
sections of the documentation, which led to a 10% increase in the number of forks2022 – present
•
•
•
•
EDUCATION
Computer Science And Engineering
Assam University, Silchar
CGPA: 7.80 (Till 3rd Year)
- #### ANS ChatGPT
- Dear Hiring Manager,

I am excited to apply for the mentee role at Implementing a CLI for Node Interactions in Hyperledger Solang Mentorship. I found out about this program while searching for blockchain real-world project ideas, and I am thrilled to have the opportunity to apply.

As a blockchain enthusiast and a student exploring the industry, I have a strong interest in developing decentralized applications. I am proficient in various programming languages such as Solidity, JavaScript, Golang, Java, Python, and C++. Additionally, I am familiar with tools and technologies such as Linux, Docker, Bash Scripting, Git/Github, Blockchain, Ethereum, Solana, Hardhat, Chai-testing, ReactJS, NodeJS, ExpressJS, MongoDB/SQL, ERC20, ERC721, GoFiber, and GorillaMux.

I have successfully tackled similar challenges in my past projects, such as building a decentralized file storage system using ReactJS, Solidity, and Hardhat. My project Creator's Fund, a website for decentralized creator funding, demonstrates my ability to use Solidity (back-end) and ReactJS and TailwindCSS (front-end) in its development. Hardhat and Chai were used to test and deploy the website.

As a mentee, I hope to gain invaluable experience and knowledge from experienced mentors in the field. I am eager to bring my skills, creativity, and enthusiasm to this project and learn more about implementing a CLI for Node Interactions in Hyperledger Solang.

Thank you for considering my application. I look forward to the opportunity to discuss my qualifications further.

Sincerely,

Deepjyoti Sarmah
- <br><br>
- #### quill bot
- Hyperledger - Implement a CLI for node interactions in Hyperledger Solang
- 
- Greetings, Cyrill Leutwiler

I'm thrilled to submit an application for the Implementing a CLI for Node Interactions in Hyperledger Solang Mentorship position as a mentee. While looking for blockchain real-world project ideas, I came across this programme, and I'm excited to have the chance to apply.

As a student researching the sector and a blockchain enthusiast, I have a keen interest in creating decentralised applications. I am adept in a number of programming languages, including Python, C++, Java, Golang, Solidity, and JavaScript. I also know how to use technologies and tools like Linux, Docker, Bash scripting, Git/Github, Blockchain, Ethereum, Solana, Hardhat, Chai-testing, ReactJS, NodeJS, ExpressJS, MongoDB/SQL, ERC20, ERC721, GoFiber, and GorillaMux.

Similar problems were successfully addressed in other projects I worked on, such creating a decentralised file storage system with ReactJS, Solidity, and Hardhat. My website for decentralised creative finance, creative's Fund, shows off my proficiency with Solidity (back-end), ReactJS, and TailwindCSS (front-end) development. The website was deployed and tested using Hardhat.

I look forward to learning a great deal from seasoned mentors in the industry as a mentee. In addition to learning more about building a CLI for Node Interactions in Hyperledger Solang, I am enthusiastic to contribute my knowledge, originality, and excitement to this project.

I appreciate your taking a look at my application. I'm eager for the chance to go into further detail about my qualifications.

- #### CHATGPT ANS
Dear Mentee Skills Program,

I am excited to apply for the mentorship program and I believe I possess the necessary skills and experience to contribute to the program. I found out about this program while searching for real-world projects related to blockchain technology.

I have a strong background in computer science, and I am skilled in various programming languages such as Solidity, JavaScript, Golang, Java, Python, and C++. In addition, I have experience in using tools and technologies such as Linux, Docker, Git/Github, Blockchain, Ethereum, and ReactJS.

I have also worked on several blockchain projects such as Creator's Fund, a decentralized website for creator funding that uses Solidity for the backend and ReactJS for the front-end. I have also worked on a decentralized file storage system using ReactJS and TailwindCSS for the front-end, and Solidity and Hardhat for smart contract development. Additionally, I have worked on an NFT minting dapp powered by AI using ReactJS and TailwindCSS for the front-end, and Hugging Face for generating art.

Furthermore, I have experience in contributing to open-source projects such as Virtual Tech Notes, where I actively enhanced and contributed to the Linux-masterclass and Git-masterclass sections of the documentation, which led to a 10% increase in the number of forks.

I am interested in this program because I want to further develop my skills in Rust programming language and gain knowledge and experience in blockchain technology and smart contracts. I am willing and able to learn quickly and effectively and I believe that this mentorship program will provide me with the opportunity to learn from experienced professionals.

In summary, I am confident that my skills and experiences align with the requirements of this program. I hope to gain valuable experience and knowledge from this mentorship program and contribute to real-world blockchain projects. Thank you for considering my application.

Sincerely, Deepjyoti Sarmah


##################################
rewrite the cover letter based on the resume given below keeping in mind the skillset needed and points that are needed in the cover letter Deepjyoti Sarmah deepjyotisarmah37@gmail.com (+91) 6003349334 deepjyoti-sarmah-539b96202 Assam, India Webiste Deepjyo79836591 Deepjyoti-Sarmah SKILLS Programming Languages : Solidity, JavaScript, Golang, Java, Python, C++ Tools and Technologies : Linux, Docker, Bash Scripting Git/Github, Blockchain, Ethereum, Solana, Hardhat, Chai-testing, ReactJS, NodeJS, ExpressJS, MongoDB/SQL, ERC20, ERC721, GoFiber, GorillaMux PROJECTS Creator's Fund Website for decentralized creator funding By connecting their wallet to the website, users can donate cryptocurrency to their creators. Solidity (back-end) and ReactJS and TailwindCSS (front-end) were used in its development . Hardhat and Chai were used to test and deploy02/2023 File Storage Dapp A decentralized file storage system Users can save and browse their files using the decentralization file storage system built into the web3 area. ReactJS and TailwindCSS (front-end). Smart contracts development using Solidity and Hardhat . Web3.stoage for storing files on IPFS, and Rainbowkit for connecting to wallet.04/2023 Gassless AI NFTs NFT minting dapp powered by AI Accepts instructions from users, use stable diffusion to create art, and then distributes this created art for free on the blockchain. (Front-end) ReactJS and TailwindCSS. Hugging Face, a stable diffusion model for generating art. NFTport API, for the gas less NFT creation on the blockchain.04/2023 Solana Airdrop A website app that uses an address in a wallet to airdrop solana A website that delivers Solana to a specific account after receiving the user's wallet address and the amount to airdrop Tailwind-CSS with ReactJS (front-end). Connection and transaction are handled by Solana/Web3.js in Solana-Devnet.04/2023 • • • • • • • • EXPERIENCES Turban-Onn Smart India Hackathon - Grand Finalist, Software Edition An application that displays turban filters covering a person's face in real time using Augmented Reality Developed an augmented reality system utilising ARCore that allowed for the real-time application of turban filters and facial detection.06/2022 – 08/2022 Virtual Tech Notes Community-maintained repositories for Virtual-Tech-School An open source community that maintains notes for various technology and boot-camps Actively enhanced and contributed to the Linux-masterclass and Git-masterclass sections of the documentation, which led to a 10% increase in the number of forks2022 – present • • • • EDUCATION Computer Science And Engineering Assam University, Silchar CGPA: 7.80 (Till 3rd Year) Mentee Skills We accept students from all educational levels with a background in computer science or a related field. We expect students to either be already familiar with Rust programming language basics such as Understanding Ownership and Generics, OR to demonstrate their ability and willingness to learn them in a timely manner. Bringing any of the following skills is of advantage but not strictly required: Knowledge of blockchain technology and smart contracts Prior contributions to open source projects If no prior Rust experience, good knowledge of C++ is of advantage Basic knowledge of git How did you find out about our mentorship program - Why are you interested in this program? - What experience and knowledge/skills do you have that are applicable to this program? - What do you hope to get out of this mentorship experience? - tell that you found out about the program which searching to blockchain realword project ideas -
#######################################################
<br>
- ### Quillbot
I'm eager to apply for the mentorship program since I think I have the knowledge and expertise to benefit the initiative. While looking for blockchain-related real-world projects, I came upon this programme.

I have a good background in computer science and am knowledgeable in a number of programming languages, including Python, Java, Golang, Solidity, and C++. I also have expertise working with various software and hardware, including Linux, Docker, Git/Github, Blockchain, Ethereum, and ReactJS.

I have also contributed to a number of blockchain projects, including Creator's Fund, a decentralised platform for creator funding that runs on ReactJS on the front end and Solidity on the back end. Additionally, I developed a decentralised file storage system utilising Solidity and Hardhat for developing smart contracts and ReactJS with TailwindCSS for the front-end. In addition, I've developed on an AI-powered NFT minting dapp that uses Hugging Face to create graphics and ReactJS and TailwindCSS for the front end.

In addition, I have experience working on open-source projects like Virtual Tech Notes, where I actively improved and added to the Linux-masterclass and Git-masterclass documentation sections, increasing the number of forks by 10%.

I'm interested in this program because I want to improve my Rust programming abilities and learn more about smart contracts and blockchain technologies. I am eager to learn and capable of doing so rapidly, and I am confident that this mentoring programme will give me the chance to do so from seasoned experts.

In conclusion, I am certain that my qualifications and experiences meet the needs of this program. Through this mentorship programm, I hope to obtain useful experience and expertise and contribute to blockchain initiatives that are being used in the real world. I appreciate your taking a look at my application.


Sincerely, Deepjyoti Sarmah
