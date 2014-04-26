documentation (draft)
===================

```
class Scene1 < ExplorationScene
  SPOON = [:spoon, position: [330, 30], size: [60, 50]]
  
  def start
    invite :bob, :alice # is it really useful? I don't know yet
    
    go_to :start
    run
  end
  
  def scenario(division)
    case division
      
    when :start
      background :background1
      install_items SPOON # you can also use items from other scenes (Scene2::LAMP)
      
      # background_music :suspens_music
      
      dialog :bob, {sprite: :bob_happy}, [
        "Hi! Long time no see!",
        "I was in the neighbourhood."
      ]
      
      # background :background2
      
      question :bob, {sprite: :bob_surprised}, [
        "How are you?"
      ]
      answer [
        {text: "I'm fine", go_to: :im_good},
        {text: "Not that good.", go_to: :im_not_good}
      ]
      
    when :im_good
      effect -> {
        # Mood.increase(+1)
      }
      
      dialog :bob, {sprite: :bob_happy}, [
        "Good!"
      ]
      
      go_to :lets_grab_the_spoon
      
    when :im_not_good
      effect -> {
        # Mood.increase(-1)
      }
      
      dialog :bob, {sprite: :bob_sorry}, [
        "Oh, I'm sorry."
      ]
      
      go_to :lets_grab_the_spoon
      
    when :lets_grab_the_spoon
      dialog :bob, {sprite: :bob_happy}, [
        "Can you grab me the spoon on the table?"
      ]
      
      explore -> {
        inventory.has?(:spoon)
      }
      
      dialog :bob, {sprite: :bob_happy}, [
        "Thank you!",
        "Let's go to Scene 2!"
      ]
      
      go_to Scene2
      
    end
  end
end
```