import customtkinter as ctk
import random
import tkinter.messagebox as messagebox


class Main:
    def __init__(self, title="Robot Demonstration", width=600, height=600):
        self.window = ctk.CTk()
        self.window.geometry(f"{width}x{height}")
        self.window.title(title)

        buttonRed = ctk.CTkButton(self.window, text="Insert Red", fg_color="red", text_color="black")
        buttonGreen = ctk.CTkButton(self.window, text="Insert Green", fg_color="lime", text_color="black")
        buttonBlue = ctk.CTkButton(self.window, text="Insert Blue", fg_color="cyan", text_color="black")
        buttonYellow = ctk.CTkButton(self.window, text="Insert Yellow", fg_color="yellow", text_color="black")

        buttonRed.grid(column=0, row=0, pady=20)
        buttonGreen.grid(column=1, row=0, pady=20)
        buttonBlue.grid(column=2, row=0, pady=20)
        buttonYellow.grid(column=3, row=0, pady=20)

        self.canvas = ctk.CTkCanvas(self.window, width=100, height=100)
        self.canvas.grid(column=1, columnspan=2, row=1, pady=20)

        self.rectangle = self.canvas.create_rectangle(0, 0, 150, 150, fill="red")

        self.canvas.itemconfig(self.rectangle, fill="red")  # change fill to display what color it thinks it is

        # Bind the buttons to their respective click handlers
        buttonRed.bind("<Button-1>", lambda event: self.change_rectangle_color("red"))
        buttonGreen.bind("<Button-1>", lambda event: self.change_rectangle_color("lime"))
        buttonBlue.bind("<Button-1>", lambda event: self.change_rectangle_color("cyan"))
        buttonYellow.bind("<Button-1>", lambda event: self.change_rectangle_color("yellow"))

        labelRedNest = ctk.CTkLabel(self.window, text="Red Nest", fg_color="transparent", text_color="white")
        labelGreenNest = ctk.CTkLabel(self.window, text="Green Nest", fg_color="transparent", text_color="white")
        labelBlueNest = ctk.CTkLabel(self.window, text="Blue Nest", fg_color="transparent", text_color="white")
        labelYellowNest = ctk.CTkLabel(self.window, text="Yellow Nest", fg_color="transparent", text_color="white")

        labelRedNest.grid(column=0, row=2)
        labelGreenNest.grid(column=1, row=2)
        labelBlueNest.grid(column=2, row=2)
        labelYellowNest.grid(column=3, row=2)

        self.labels = {
            "red": labelRedNest,
            "lime": labelGreenNest,
            "cyan": labelBlueNest,
            "yellow": labelYellowNest
        }

        self.correct_label_color_pairs = {}

        self.window.mainloop()

    def change_rectangle_color(self, color):
        """Changes the fill color of the rectangle to the specified color."""
        self.canvas.itemconfig(self.rectangle, fill=color)

        unmatched_labels = {key: value for key, value in self.labels.items() if
                            key not in self.correct_label_color_pairs}
        if not unmatched_labels:
            messagebox.showinfo("All matched", "All colors have been correctly assigned to their respective labels.")
            return

        random_label_color = random.choice(list(unmatched_labels.keys()))
        random_label = unmatched_labels[random_label_color]
        random_label.configure(fg_color=color)

        user_answer = messagebox.askyesno("Color Assignment",
                                          f"Is the assigned color ({color}) correct for the {random_label_color.capitalize()} Nest?")
        if user_answer:
            self.correct_label_color_pairs[random_label_color] = color
            random_label.configure(fg_color=color, text_color="black")
        else:
            random_label.configure(fg_color="transparent")


if __name__ == '__main__':
    Main()

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Pentru a putea rula acest cod este necesar de a instala pycharm si bibliotecile customtkinter si tkinter.messagebox.
Este necesara detinerea unui set de LEGO MINDSTORM ROBOT INVENTOR altfel aplicatia nu v-a functiona












    
