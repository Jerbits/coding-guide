
![e0689d4028e2205ee56399cca6c5608e](https://github.com/Jerbits/coding-guide/assets/34278217/94160398-3214-46ac-8a0b-8fa0acbaef41)


# 💻   My Frontend Cheatsheet

## Table of Contents

 1. [Introduction](#introduction)
 2. [Naming Conventions](#naming-conventions)
 3. [Writing Functions](#writing-functions)
 4. [React Components](#react-components)
 5. [CSS and Tailwind](#css-and-tailwind)
 6. [Formatting](#formatting)
 7. [Testing](#testing)
 8. [Asset Optimization](#asset-optimization)
 9. [Packages and Libraries](#packages-and-libraries)


## Introduction
My accumulated list of how-tos, guides, and cheatsheets from my experience working with different companies

## Naming Conventions

### **💡 Variable names should be lower camel case**

❌ BAD:

    let FunctionName;
    let variable_name;
    let UsEr;
    
✅ GOOD: 

    let functionName;
    let variableName;
    let user;

### **💡 Types should be pascal case with a prefix indicating the kind of type it is**

❌ BAD:

    interface userProps;
    type Cool_types;
    enum Direction {
	  Up,
	  Down,
	  Left,
	  Right
	}
    
✅ GOOD:

    interface IUserProps;
    type TCoolTypes;
    enum EDirection {
	  Up,
	  Down,
	  Left,
	  Right
	}

### **💡 Constants and Enums should be capitalized and snake cased**

❌ BAD:

    const imageCfg = {...image_configuration} as const;
    const carouselData = [Object, Object]
    enum MY_ENUM
    
✅ GOOD:

    const IMAGE_CONFIGURATION = {...image_configuration} as const;
    const CAROUSEL_CONTENT = [Object, Object]
    enum EMyEnum


### **💡 Avoid adding unnecessary context**
*Choosing descriptive names for variables and functions enhances code readability and reduces the need for explanatory comments. The variable name 'data' should be replaced with something explanatory*

❌ BAD:


    const user = {
		userAccountName: 'jerome',
		userAccountId: 'jerome123',
		userAccountAddress: 'Canada On',
	}


✅ GOOD:


     const user = {
		name: 'jerome',
		id: 'jerome123',
		address: 'Canada On',
	}


### **💡 Abbreviations and acronyms should not be uppercase when used as a (OR part of a) name.**

❌ BAD:

    const parsedHTMLString = parserFunction(someString);
    const userID = 'Jerome123'

✅ GOOD:

    const parsedHtmlString = parserFunction(someString);
    const userId = 'Jerome123'


### **💡 Booleans should have prefix identifiers**
*Using the 'is/has/can/was' prefix solves a common problem of choosing bad boolean names like status or flag*

❌ BAD:

    const active = true;
    const valid = true;
    const access = true;
    const permission = true;
    const exit = true;
    const deleted = true;

✅ GOOD:

    const isActive = true;
    const isValid = true;
    const hasAccess = true;
    const hasPermission = true;
    const canExit = true;
    const wasDeleted = true;

### **💡 Methods and Functions should be using verbs**

❌ BAD:

    const toggleNow = () => {};
    const nameIt = () => {};
    const whatIsMyMaxValuePlease = () => {};

✅ GOOD:

    const handleToggle = () => {};
    const getName = () => {};
    const computeMaxValue = () => {};

### **💡 Variable representing a collection should be plural**

❌ BAD:

    const asset = [image, video, svg];
    const parsedAssetArray = asset.map((ast) => `cool-${ast}`);

✅ GOOD:

    const assets = [image, video, svg];
    const parsedAssets = assets.map((asset) => `cool-${asset}`);

***Exception**: Iteration variables don't have to be descriptive when used in small well-encapsulated functions and methods* 

### **💡 Use descriptive and meaningful variable names**

*Choosing descriptive names for variables and functions enhances code readability and reduces the need for explanatory comments. The variable name 'data' should be replaced with something explanatory*

❌ BAD:


    const total = (data) => {
      let total = 0;
      for (let i = 0; i < data.length; i++) {
        total += data[i].value;
      }
    
      return total;
    }


✅ GOOD:


    const getAccountsTotalBalance = (accounts) => {
      let totalBalance = 0;
      for (let accountIndex = 0; accountIndex < accounts.length; accountIndex++) {
        totalBalance += accounts[accountIndex].balance;
      }
    
      return totalBalance;
    }

***Exception**: Iteration variables don't have to be descriptive when used in small well-encapsulated functions and methods* 

### **💡 Don't be cute**

*Avoid using slang*

❌ BAD:

    process.whack()

✅ GOOD:

    process.kill()

### **💡 Avoid negative names for standalone variables**

*When naming booleans, you should avoid choosing variable names that include negations. It’s better to name the variable _without_ the negation and flip the value. This requires the person reading the code to perform a logical negation twice.*

❌ BAD:

    const hasNoAccess = accounts.length === 0;

✅ GOOD:

    const hasAccess = accounts.length > 0;


## Writing Functions

### **💡 Use arrow functions when the `this` keyword is not used**

*Arrow functions do not bind their own `this`, instead, they inherit the one from the parent scope, which is called "lexical scoping". Arrow functions should ideally be always used when writing a functional component*

✅ EXAMPLE 1:

    const myObject = { 
	    myMethod: function () {
		    console.log('function')
		} 
	};
   
   ✅ EXAMPLE 2:

       const myFunction = () => {console.log('Arrow function')}



### **💡 Keep function arguments to 3 or less (the fewer the better)**

*Reducing the number of function parameters is of great significance as it simplifies testing. Exceeding three parameters results in a complex web of test cases, adding to the testing workload.*

❌ BAD:

    const handleModal = (title: string, body: string, subtext: string, isActive: boolean) => { ... };

✅ GOOD:

    const handleModalContent = (title: string, body: string, subtext: string) => { ... };
    const handleModalToggle = (isActive: boolean) => { ... };

### **💡 Keep functions pure**

*Write small and simple functions that avoid side effects. Functions that always return the same result are easier to test*

❌ BAD:


    const addParameter = 3;
    
    const getSumPlusParameter = (a, b) => {
      return a + b + addParameter;
    };

✅ GOOD:

    const getSum = (a, b) => {
      return a + b;
    };

### **💡 A function should do one thing and do it well**

*Functions should do one thing. When a function does more than one thing it makes reading and testing harder.*

❌ BAD:

     const handleCarousel = (title: string, image: string, isActive: boolean, carouselIndex: number) => { ... };

✅ GOOD:

    const handleCarouselContent = (title: string, image: string) => { ... };
    const handleCarouselToggle = (isActive: boolean, carouselIndex: number) => { ... };


### **💡 Function names should be descriptive and intention revealing**

-   Functions that affect only logic and are not coupled to a UI should be descriptive of that purpose e.g.  `incrementCarouselIndex`, `computeTotalValue`, `getMaxWidth`.
-   For functions that are tied to a UI, it should be named by what the UI does e.g. `advanceCarouselImage`, `hideCarouselButton`, `disableButton`.


### **💡 Use default argument values when meaningful**

_If a value can be undefined make the arg optional_

❌ BAD:

     const incrementCarouselIndex = (carouselIndex: number) => { 
	     if(!carouselIndex) {
			carouselIndex = 1
		}
     };

✅ GOOD:

    const incrementCarouselIndex = (carouselIndex: number = 1) => { 
		...
     };

***NOTE**: this is a contrived example. Don't mutate external variables to avoid side-effects*


## React Components

### **💡Folder structure that accounts for external files**

*A consistent folder structure helps team members collaborate more efficiently by providing a shared understanding of where files are located. This makes it easier to work on the same files and avoid conflicts.*

✅ EXAMPLE 1:

    src/  
	    |-  components/  
		    |-  ComponentNameA/  
			    |-  ComponentNameA.tsx  
			    |-  component-name-a.scss  
			    |-  ComponentNameA.test.tsx  
			    |-  index.ts  
			    |-  NestedComponent/  (A  component  used  only  in  ComponentA)  
				    |-  NestedComponent.tsx  
				    |-  Nested-component-name.scss  
				    |-  NestedComponent.test.tsx  
				    |-  index.ts  
		    |-  ComponentNameB/  
			    |-  ComponentNameB.tsx  
			    |-  component-name-b.scss  
			    |-  ComponentNameB.test.tsx  
			    |-  index.ts  


### **💡Component files naming conventions**

 - Components should be Pascal case
 - Component names should be meaningful
 - Test files should be camel case
 - External stylesheets should be kebab case

❌ BAD:

    |-  nModal/  
	    |-  nModal.tsx  
	    |-  modalStyles.scss  
	    |-  nModal.test.tsx  
	    |-  index.ts   

✅ GOOD:

    |-  NotificationModal/  
    	    |-  NotificationModal.tsx  
    	    |-  notification-modal.scss  
    	    |-  NotificationModal.test.tsx  
    	    |-  index.ts
    

### **💡Keep components small and modular**

*Keeping components small and focused on a single responsibility makes it easier to test and debug code. Smaller components are easier to reuse across the application, making it easier to maintain and scale the codebase. Breaking down components into smaller parts allows you to separate ths of your application.*

❌ BAD:

        export const Payment = ({ amount }: { amount: number }) => {
        const [paymentMethods, setPaymentMethods] = useState<LocalPaymentMethod[]>(
          []
        );
      
        useEffect(() => {
          const fetchPaymentMethods = async () => {
     const url = "https://online-ordering.com/api/payment-methods";
      
            const response = await fetch(url);
            const methods: RemotePaymentMethod[] = await response.json();
      
            if (methods.length > 0) {
              const extended: LocalPaymentMethod[] = methods.map((method) => ({
     provider: method.name,
                label: `Pay with ${method.name}`,
              }));
              extended.push({ provider: "cash", label: "Pay in cash" });
              setPaymentMethods(extended);
            } else {
              setPaymentMethods([]);
            }
          };
      
          fetchPaymentMethods();
        }, []);
      
     return (
          <div>
            <h3>Payment</h3>
            <div>
              {paymentMethods.map((method) => (
     <label key={method.provider}>
                  <input
                    type="radio"
                    name="payment"
                    value={method.provider}
                    defaultChecked={method.provider === "cash"}
                  />
                  <span>{method.label}</span>
                </label>
              ))}
            </div>
            <button>${amount}</button>
          </div>
        );
      };

✅ GOOD:

    

    // useFetchPaymentMethods.ts
    export const useFetchPaymentMethods = () => {
	    const [paymentMethods, setPaymentMethods] = useState<IPaymentMethods[]>([]);
	    useEffect(() => {
		    (async () => {
		    const response = await fetch('https://api.com/api/methods');
		    const json = await response.json();
		    setMethod(json);
		})();

	    return { paymentMethods };
	    });
    };
    
    
    // Title.tsx
    export const Title = ({ children }: { children: JSX.Element }) => {
	    return <h3>{children}</h3>;
    };


    // Button.tsx
    export const Button = ({ children, type }: { children: JSX.Element; type: TButtonTypes;
    }) => {
	    return <button>{children}</button>;
    };
    
    // PaymentMethodSelectBoxes.tsx
    export  const  PaymentMethodSelectBoxes = ({
	    paymentMethods,
    }: {
	    paymentMethods: PaymentMethods[];
    }) => {
	    return (
		    <div>
			    {paymentMethods.map((method) => (
				    <label  key={method.provider}>
				    <input
					    type='radio'
					    name='payment'
					    value={method.provider}
					    defaultChecked={method.provider === 'cash'}
				    />
					    <span>{method.label}</span>
				    </label>
			    ))}
		    </div>
	    );
    };
        
    // Payment.tsx
    export const Payment = ({ amount }: { amount: number }) => {
	    const { paymentMethods } = useFetchPaymentMethods();      
	    return (
		    <div>
			    <Title>Payment</Title>
			    <PaymentMethodSelectBoxes paymentMethods={paymentMethods} />
			    <Button>${amount}</Button>
		    </div>
	    );
    };

***NOTE**: this is a contrived example. The BAD example at the top is perfectly fine because it is small and simple. But for larger complex components we should break them down into small modular pieces*


## CSS and Tailwind

### **💡Always use fewer utility classes when possible**

❌ BAD:

    <div className="ml-2 mr-2"></div>
    <div className="pt-4 lg:pt-8 pr-4 pb-4 pl-4"></div>

✅ GOOD:

    <div className="mx-2"></div>
    <div className="p-4 lg:pt-8"></div>



### **💡Use @apply to abstract multiple lines of classes to avoid duplication**

*Do not prematurely use `@apply` to abstract component classes where a proper framework/template-based component is more appropriate.*

❌ BAD:

    Component1.tsx
    <div className="flex-col flex items-start gap-5 mb-5 landscape:mobile-landscape:mb-3 sm:mb-5 md:mb-10 h-full"></div>
    Component2.tsx
    <div className="flex-col flex items-start gap-5 mb-5 landscape:mobile-landscape:mb-3 sm:mb-5 md:mb-10 h-[500px]"></div>

✅ GOOD:

    Component1.tsx
    <div className="block-component h-full"></div>
    Component2.tsx
    <div className="block-component h-[500px]"></div>
    
    global.scss
    block-component {
	    @apply flex-col flex items-start gap-5 mb-5 landscape:mobile-landscape:mb-3 sm:mb-5 md:mb-10 
    }

***NOTE**: The ideal scenario would be to keep the components modular where Component1 and Component2 are just one component and the height would be adjusted with a parameter. Modular components would also mean modular styles and we would no longer need to use @apply*


### **💡Concentric CSS**

*When writing a string of multiple utility classes, always do so in an order with meaning. 1. positioning/visibility 2. box model 3. borders 4. backgrounds 5. typography 6. Other visual adjustments. Keeping a familiar pattern helps us read and modify the classes quickly*

*Classnames of a specific category should be in the order of general to specific e.g. `flex flex-col` is better than `flex-col flex`*

❌ BAD:

    <div className="text-lg bg-black flex-col flex mb-5 sm:mb-5 md:mb-10 h-full"></div>
    

✅ GOOD:

     <div className="flex flex-col mb-5 sm:mb-5 md:mb-10 h-full bg-black text-lg"></div>
     
 
### **💡Proper use of layer directives**

*Use the `@layer` directive to tell Tailwind which “bucket” a set of custom styles belong to. Valid layers are `base`, `components`, and `utilities`.*

✅ EXAMPLE:

     @tailwind base;  
     @tailwind components;  
     @tailwind utilities;
     
     @layer base  {  h1  {  @apply text-2xl;  }  h2  {  @apply text-xl;  }  }  
     @layer components  {  .btn-blue  {  @apply bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded;  }  }  
     @layer utilities  {  .filter-none  {  filter: none;  }  .filter-grayscale  {  filter:  grayscale(100%);  }  }
 
 
### **💡Handle element spacing with Flex/Grid**

*Spacing by Flex/Grid is only added once on the parent elements versus creating multiple classes on the child elements*

❌ BAD:

    <div> 
	    <p  class="mr-2">Paragraph</p> 
	    <p  class="mr-2">Paragraph</p> 
	    <p  class="mr-2">Paragraph</p> 
	    <p  class="mr-2 last:mr-0">Paragraph</p>
    </div>
    

✅ GOOD:

     <div class="flex gap-2> 
	    <p>Paragraph</p>
	    <p>Paragraph</p> 
	    <p>Paragraph</p> 
	    <p>Paragraph</p> 
    </div>
 
### **💡Better readability using Classnames plugin**

*Improve CSS style readability by grouping utility classes with the Classnames plugin*


✅ EXAMPLE:
	
     import { default  as  cn } from  'classnames';
     
     const buttonStyle = cn( 
	     //1. positioning/visibility
	     'flex justify-center align-center',
	     // 2. box model
	     'mx-5 my-10 px-5',
	     // 3. borders
	     'border border-transparent rounded-md' 
	     // 4. backgrounds
	     'bg-black hover:bg-black/80' 
	     // 5. Typography
	     'text-sm lg:text-base xl:text-1xl'
	     
     <button className={buttonStyle} />
 
## Formatting

### **💡 Prettier config**

    {
	    "arrowParens": "always",
	    "semi": true,
	    "singleQuote": false,
	    "printWidth": 100,
	    "tabWidth": 2,
	    "proseWrap": "always",
	    "bracketSpacing": true,
	    "useTabs": false,
	    "jsxSingleQuote": true,
	    "bracketSameLine": false,
	    "trailingComma": "none"
    }


## Testing

### **💡 Unit test using Jest**
✅ EXAMPLE:
        
    function filterByTerm(inputArr, searchTerm) {
      return inputArr.filter(function(arrayElement) {
        return arrayElement.url.match(searchTerm);
      });
    }
    
    describe("Filter function", () => {
      test("it should filter by a search term (link)", () => {
        const input = [
          { id: 1, url: "https://www.url1.dev" },
          { id: 2, url: "https://www.url2.dev" },
          { id: 3, url: "https://www.link3.dev" }
        ];
    
        const output = [{ id: 3, url: "https://www.link3.dev" }];
    
        expect(filterByTerm(input, "link")).toEqual(output);
      });
    });

 
### **💡 Functional test using Jest and RTL**
✅ EXAMPLE:

    import  React  from  "react";
    import { render, screen } from  "@testing-library/react";
    import  "@testing-library/jest-dom";
    import { Header } from  "./Header";
      
    
    describe("Header", () => {
	    it("Should render the the header component", async () => {
		    // Setup
		    render(<Header  location={window.location}  />);
		    // Test
		    expect(screen.getAllByText("Home")[0]).toBeInTheDocument();
		    expect(screen.getAllByText("About")[0]).toBeInTheDocument();
		    expect(screen.getAllByText("Careers")[0]).toBeInTheDocument();
	    });
    });


## Asset Optimization

### **💡 Video Optimization for HTML Backgrounds**

_The following guidelines will help keep the video file size small:_
- Keep videos short
- Frame rate should be 25 or below
- Videos should be perfect loops to not look jarring
- Serve multiple video formats because not all browsers support the same video format
- Make sure to include an image (preferably JPEG which is widely supported) as a video fallback

### **💡 Using a poster attribute will show a custom image when the video is loading**

    <video controls poster="/images/w3html5.gif">  
	    <source src="movie.mp4"  type="video/mp4">  
	    <source src="movie.ogg"  type="video/ogg">  
	    Your browser does not support the video tag.  
    </video>
    
**Note**: The first frame of the video will be displayed if you don't use the poster attribute

### **💡 Image as a video fallback**

    <video controls poster="/images/frame.gif">  
	    <source src="movie.mp4"  type="video/mp4">  
	    <source src="movie.ogg"  type="video/ogg">  
	    <img src="/fallback.jpeg" alt="video did not load" />
    </video>

### **💡 FFMPEG as command line tool for video optimization**

https://www.ffmpeg.org/

**FFMPEG script for best browser compatibility:**
 
    ffmpeg -an -i bg-home-section-c.mp4 -vcodec libx264 -pix_fmt yuv420p -profile:v baseline -level 3 -s hd720 -crf 30 ../bg-home-section-c.mp4

**Note**: The above command line outputs an MP4 which has a CRF (Constant rate factor) of 30. CRF is an option available in the `libx264` encoder to set our desired output quality. Max CRF value is 51. The lower the value the better the quality and the bigger the file size.

### **💡 Creating a an image from a video file**

**JPEG image from the first frame of a video**

    ffmpeg -i inputfile.mkv -vf "select=eq(n\,0)" -q:v 3 output_image.jpg
    
  **JPEG image from the 10th frame of a video**

    ffmpeg -i inputfile.mkv -vf "select=eq(n\,9)" -q:v 3 output_image.jpg
    
### **💡 Creating multiple video fallbacks from video files in a folder**

    for x in $(find .); do echo && echo "[*] creating fallback"; ffmpeg -i $x -vf "select=eq(n\,5)" -q:v 3 $x.jpg ; done


### **💡 Use WebP image format when the browser supports it**

 _WebP is a modern image format that provides superior lossless and lossy compression for images on the web. It creates an image with a smaller file size while maintaining better quality than other formats_

**Further reading: [https://developers.google.com/speed/webp](https://developers.google.com/speed/webp)**

Command line Installation Instructions: [https://developers.google.com/speed/webp/docs/precompiled](https://developers.google.com/speed/webp/docs/precompiled)

[https://developers.google.com/speed/webp/docs/cwebp](https://developers.google.com/speed/webp/docs/cwebp)

**Generate WebP from a JPEG with 90% quality**
 
     cwebp -q 90 sample.jpg -o ../sample.webp


### **💡 Use a picture tag to add an image fallback when using WebP**
 
    <picture>
       <source srcset="img/asset.webp" type="image/webp" media="(min-width: 2800px)">
       <img src="img/fallback.png">
    </picture>


### **💡 Use SVG files assets that are vector formats (Icons, Logos, etc)**
 
  _SVG files store images more efficiently than common raster formats if the image isn’t too detailed. SVG files contain enough information to display vectors at any scale, whereas bitmaps require larger files for scaled-up versions of images — more pixels use more file space_

_**Note:** Don't use SVG for raster images_

### **💡 Use the ImageOptim tool to do a lossless optimization on your assets**
 
ImageOptim is a user-friendly asset optimization tool that will also strip out your asset's EXIF metadata. Ideally, you will use this tool after you have finalized the quality and target resolution for your images e.g 4k, 2k, 1080p (for responsive web images)

### **💡 Image Formats**
 
These image formats should be used based on how the images are utilized on your website.
1. SVGs - for logos and icons
2. PNGs - Raster images with transparency
3. JPEGs/WEBP - Raster images without transparency
4. GIFs - Animated images

### **💡 Use SVGR to use SVG files in your react app**
 
 https://react-svgr.com/
 
  _SVGR handles all type of SVG and transforms it into a React component._

    import { ReactComponent  as  TwitterIcon } from  '@Icons/twitter.svg';
    
    <TwitterIcon className='fill-black w-10 h-10' />

## Packages and Libraries

### **💡 Wrap libraries in an abstraction layer**

Let's say you use a library in your code that handles analytics tracking. There are hundreds of these tracking calls all over your code base. If for some reason the library decided to upgrade its package and rename the tracking call to something else, this would mean you will have to grep your entire codebase to replace this call.

To avoid this tedious process we should wrap third-party libraries with an abstraction layer. So when there is a need to update a package it will only be done within the abstraction layer and not on each individual file that uses the library.

✅ EXAMPLE:


Abstraction layer: useTracker.tsx
    
    import tracker from 'thirdparty/script';
    
    export  const  useTracker = () => {
	    const trackButton = () => {
			tracker('track this button')
		}
		return { trackButton }
    }

    
Components

    import { useTracker } from  './useTracker';
    const Component = () => {
		const { trackButton } = useTracker();
		...
		return <Button onClick={() => { trackButton() }}>
	}
    
