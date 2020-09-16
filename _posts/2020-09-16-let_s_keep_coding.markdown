---
layout: post
title:      "Let’s keep coding"
date:       2020-09-16 13:52:30 -0400
permalink:  let_s_keep_coding
---


Initial Thoughts

I’m really satisfied with how the Mod 3 project went because I felt like I was able to recreate the image I had inside my head. There are always ways to improve but the pieces that are fundamental work as I had intended. 

What I Learned

Having the models and their relations before starting the project helped give me an idea of a list of steps of what needed to be made in what order. Having that list made it quick to move on to the next step. One thing I need to get better at is realizing when I need to add more attributes because I spent way too much time trying to be “efficient” with one attribute. Once I decided to add the other attributes I should’ve had from the start, the custom validations I attempted to code earlier became much easier to write. 

The most relevant thing I learned, when it comes to this project, is the html needed to make a table and display information to that table. Thanks to playing around I learned how to separate different objects based on certain conditions to give a better user experience.

```
<table style="width:100%">
    <tr>
        <td> <h4> Completion Status </h4> </td>
        <td> <h4> Tournament Name </h4> </td>
        <td> <h4> Tournament Date </h4> </td> 
        <td> <h4> Info </h4> </td>
        <td> <h4> Tournament Link </h4> </td>
    </tr>

        <td> <h4> Incompleted Tournaments </h4> </td>
        <% @tournaments.each do |t| %>
            <tr>
                <% if t.finished == false %>
                    <td> Needs Work </td>
                    <td> <%= t.event_name %> </td>
                    <td> <%= t.event_date %> </td>
                    <td> <%= t.info %> </td>
                    <td> <%= link_to "View Tournament", tournament_path(t) %> <br> </td>
                <% end %>
            </tr>
        <% end %> 

        <td> <h4> Completed Tournaments </h4> </td>
        <% @tournaments.each do |t| %>
            <tr>
                <% if t.finished == true %>
                    <td> Complete </td>
                    <td> <%= t.event_name %> </td>
                    <td> <%= t.event_date %> </td>
                    <td> <%= t.info %> </td>
                    <td> <%= link_to "View Tournament", tournament_path(t) %> <br> </td>
                <% end %>
            </tr>
        <% end %>
    
    </table>
```

With two if conditions I can separate which tournaments are unfinished and should show up at the top vs ones that are finished and of less importance.

A separate feature that I implemented was allowing the user to determine how many card (child) objects are created for their deck (parent) object. 

``` 
@deck = Deck.new
Deck.row("new").times { @deck.cards.build }
```

A child object is built x amount of times based on a variable in the Deck Class. 

```
    @rows = 20
    @edit_rows = 1

    def self.row_increase(action)
        if action == "new"
            @rows += 1
        elsif action == "edit"
            @edit_rows += 1 
        end 
    end

    def self.row_decrease(action)
        if action == "new"
            @rows -= 1
        elsif action == "edit"
            @edit_rows -= 1 
        end 
    end

    def self.row(action)
        if action == "new"
            @rows 
        elsif action == "edit"
            
            @edit_rows 
        end 
    end
```

The row increase and decrease actions are called by Add Card and Remove Card buttons in the new/edit forms.

```
     def add_cards
        if params[:deck_id].present?
            Deck.row_increase("edit")
            redirect_to edit_deck_path(params[:deck_id])
        else
            Deck.row_increase("new")
            redirect_to new_deck_path
        end 
    end

    def remove_cards
        if params[:deck_id].present?
            Deck.row_decrease("edit")
            redirect_to edit_deck_path(params[:deck_id])
        else
            Deck.row_decrease("new")
            redirect_to new_deck_path
        end 
    end
```

Last Thoughts

Even though I'm happy with how this project turned out I know there's better and that when I know better I can improve upon it. For now, I'll take this achievement and show off that I made this.
