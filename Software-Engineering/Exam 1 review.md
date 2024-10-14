# Development Approaches and Concepts

## Big Bang Approach to Development
- **Description**: The Big Bang approach is a straightforward software development method where the entire project is built in one single phase without prior planning or iterative development. It relies heavily on the developer’s ability to understand all requirements and integrate them cohesively at once.
- **Path Taken**: This approach involves gathering all the requirements at the beginning and then proceeding to implement everything in one go without intermediate milestones or testing phases. The software is tested after all the development is completed.
- **Disadvantages**: This method carries high risk since there is no room for feedback during the development process. If any requirements are misunderstood or changed, significant portions of the project may need rework. It often leads to failed projects or massive overruns in time and cost due to poor control over complexity.

## Iterative Approach to Development
- **Description**: The Iterative approach breaks down the software development process into small, manageable cycles. Each iteration includes planning, designing, coding, testing, and integrating parts of the software, allowing for regular adjustments based on client feedback.
- **Path Taken**: Each iteration involves developing a working piece of the software with the goal of gradually improving upon it. This results in a cumulative build-up of features, leading to a complete product over time. New iterations can address shortcomings or changes identified from the previous one.
- **Advantages**: This method allows for constant user feedback, reduces risk, and ensures that evolving customer needs are met. It also promotes continuous improvement and faster identification of problems.

## Role of the Customer/Client
- **Role**: The customer plays a crucial role throughout the software development lifecycle. They provide requirements, participate in planning and feedback cycles, and validate the software's ability to meet their needs. Their involvement ensures that the product evolves in alignment with their expectations, reducing the likelihood of surprises at the end.

## User Stories
- **All Parts**: A user story typically consists of a title, description, priority, and an estimate.
- **Description**: User stories are short descriptions of a feature from an end-user perspective. They capture the "who," "what," and "why" of a product feature in plain language.
- **Creation**: User stories are created collaboratively between the customer, developers, and other stakeholders. The goal is to create a shared understanding of the software requirements.
- **Valid User Story Titles**: Examples include "User Registration," "Password Reset," "Product Search," etc.

## Use Case
- **Diagram and Text**: A use case includes both a visual representation (typically in UML) and a textual description outlining the interactions between a user and the system to achieve a specific goal.
- **Differences with User Stories**: While user stories capture what users want from the system in a conversational format, use cases offer a detailed sequence of interactions to achieve specific functionality.

## Estimates and Estimation Process
- **Planning Poker**: Planning poker is an estimation technique where team members assign effort points to user stories using numbered cards. The goal is to converge on an estimate through consensus, minimizing cognitive biases.

## Iteration and Deadline Planning
- **Description**: Planning iterations involve breaking down features into smaller deliverable components, assigning deadlines, and setting milestones to ensure timely progress.

## Utopian vs. Real-World Days
- **Utopian Days**: The ideal development time assuming no interruptions or issues.
- **Real-World Days**: Time required considering real-world distractions, meetings, and unexpected challenges.

## Velocity
- **Description**: Velocity is a metric that represents the amount of work a team can complete in an iteration. It helps predict future capacity and progress.
- **Standard Rate**: The velocity should stabilize over time, allowing for accurate future estimates.
- **Meaning**: If velocity is higher, it might indicate improved efficiency or oversimplified estimates. Lower velocity could indicate difficulties or underestimation of complexity.

## Big Board
- **Basics**: A Big Board, like a Kanban board, visualizes the status of tasks in a project. It shows which tasks are pending, in progress, or complete.
- **Usage by Developers**: Developers move their task cards across the board to indicate progress, making the project status visible to everyone.

## Good-Enough Design, SRP, DRY
- **Good-Enough Design**: Focuses on delivering workable solutions quickly rather than striving for perfection, ensuring progress continues smoothly.
- **SRP (Single Responsibility Principle)**: Each module or class should have one clear purpose or responsibility.
- **DRY (Don't Repeat Yourself)**: This principle promotes avoiding duplicate code by abstracting repeated functionalities into reusable components.

## Version Control
- **Jobs**: Keeps track of all changes made to files, enables collaboration, ensures that code is safe in a repository, and facilitates merging changes.
- **Commit Messages**: Should be clear and describe the purpose of the changes made.
- **Branches**: Branches are used to manage independent lines of development. Features, bug fixes, and experiments can be handled separately without affecting the main codebase.

## Dumb Questions (Chapters 1-6)

### Chapter 1: Great Software Development
- **Q: Why is pleasing the customer important?**
  - **A**: If the customer is unhappy, the software is considered a failure regardless of its technical quality. Happy customers lead to successful projects.
- **Q: Can I just build what the customer asks for?**
  - **A**: No, often customers don’t know exactly what they want or need. Developers must help clarify requirements and iterate based on feedback.

### Chapter 2: Gathering Requirements
- **Q: How do I know if I have all the requirements?**
  - **A**: You likely won't have all the requirements upfront. Requirements evolve over time as customers see the product and provide feedback.
- **Q: What if the customer keeps changing their mind?**
  - **A**: Iterative development helps manage changing requirements by allowing flexibility and adjustments in each iteration.

### Chapter 3: Project Planning
- **Q: Why do we need to prioritize requirements?**
  - **A**: Prioritizing ensures that the most important features are developed first, allowing for early feedback and ensuring key functionalities are delivered.
- **Q: Can’t we just add more people to meet deadlines?**
  - **A**: Adding more people can sometimes slow down progress due to the increased need for communication and integration.

### Chapter 4: User Stories and Tasks
- **Q: Why are user stories important?**
  - **A**: User stories help capture what the customer needs in simple language, ensuring everyone on the team has a shared understanding of the feature.
- **Q: What if a user story is too big?**
  - **A**: Large user stories, also known as epics, should be broken down into smaller, more manageable stories that can be completed within an iteration.

### Chapter 5: Good-Enough Design
- **Q: Isn’t perfect design the goal?**
  - **A**: Striving for perfect design can lead to delays and over-engineering. Good-enough design focuses on meeting requirements efficiently and evolving as needed.
- **Q: How do I know if my design is good enough?**
  - **A**: If the design solves the problem, meets requirements, and allows for future changes, it’s good enough.

### Chapter 6: Version Control
- **Q: Why do I need version control?**
  - **A**: Version control helps manage changes, prevent data loss, and facilitate collaboration among team members.
- **Q: What if two people change the same file?**
  - **A**: Version control systems help merge changes and handle conflicts, ensuring everyone’s work is integrated properly.